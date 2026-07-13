# Medallion Architecture: The Data Transformation Pipeline

**Author:** Jennifer Kelleman
**Platform:** Microsoft Fabric (Data Factory + Spark Notebooks + Lakehouse)

---

## What Is the Medallion Architecture?

The medallion architecture is a data design pattern that organizes data into progressive quality zones:

- **Bronze** — Raw, as-ingested data. Immutable. Preserves the source record.
- **Silver** — Cleaned, conformed, and validated. The governed record.
- **Gold** — Business-optimized views. The analytics and AI record.

It's a deceptively simple framework. The reason it's worth doing the architecture document is that the *decisions inside each layer* — what gets transformed, when, by what rules, and validated by what criteria — are where programs succeed or fail.

This document walks through how each layer is implemented on Microsoft Fabric, what the transformation logic looks like, and — critically — how you explain each layer to an executive audience.

---

## The Executive Narrative for Each Layer

Before diving into the technical implementation, here's how each layer maps to an executive-level story:

| Layer | Technical Description | Executive Narrative |
|---|---|---|
| **Bronze** | Raw data landed in OneLake | "We have a complete, immutable record of everything your systems produce. Nothing is lost." |
| **Silver** | Cleaned and conformed data | "We know which data is trustworthy and which isn't — and we have the proof." |
| **Gold** | Business-ready curated views | "Your analysts and AI applications are working from the same trusted, purpose-built datasets." |

These aren't just translations — they're the three commitments of a mature data estate. Executives care about completeness, trust, and readiness. That's the story.

---

## Bronze Layer: Ingest with Fidelity

### Design Principles
1. **Land everything, transform nothing.** Bronze tables preserve the source record as-is.
2. **Schema-on-read where possible.** Use Delta inference for structured sources; preserve raw JSON/CSV in Files zone for unstructured.
3. **Capture metadata at ingest.** Every Bronze record gets `_ingest_timestamp`, `_source_system`, and `_pipeline_run_id` columns added.

### Data Factory Pipeline Pattern

The standard Bronze ingestion pipeline uses the following pattern:

```
[Source Connector] → [Copy Activity] → [Bronze Delta Table]
         ↓                                       ↓
  Schema Mapping                        Add Audit Columns
  (source → bronze)               (_ingest_timestamp, _source_system, _pipeline_run_id)
```

**Pipeline configuration (Data Factory):**

```json
{
  "name": "bronze_ingest_[source_system]",
  "activities": [
    {
      "name": "CopyFromSource",
      "type": "Copy",
      "source": {
        "type": "SqlSource",
        "sqlReaderQuery": "SELECT *, GETDATE() as _extract_timestamp FROM [schema].[table]"
      },
      "sink": {
        "type": "LakehouseTableSink",
        "tableOption": "autoCreate",
        "writeBehavior": "append"
      }
    }
  ],
  "parameters": {
    "source_system": { "type": "string" },
    "table_name": { "type": "string" },
    "watermark_column": { "type": "string", "defaultValue": "modified_date" }
  }
}
```

### Watermark-Based Incremental Load

For source systems with high-volume tables, Bronze ingestion uses a watermark pattern:

```python
# Watermark-based incremental load (Fabric Notebook, PySpark)
from pyspark.sql import functions as F
from delta.tables import DeltaTable

# Read current high-water mark from control table
watermark_df = spark.sql("""
    SELECT MAX(watermark_value) as last_watermark
    FROM platform_services.pipeline_control
    WHERE source_system = '{source_system}' AND table_name = '{table_name}'
""")
last_watermark = watermark_df.collect()[0]["last_watermark"]

# Incremental extract
new_records = spark.read.jdbc(
    url=source_jdbc_url,
    table=f"(SELECT * FROM {schema}.{table_name} WHERE {watermark_col} > '{last_watermark}') t",
    properties=jdbc_properties
).withColumn("_ingest_timestamp", F.current_timestamp()) \
 .withColumn("_source_system", F.lit(source_system)) \
 .withColumn("_pipeline_run_id", F.lit(pipeline_run_id))

# Append to Bronze Delta table
new_records.write.format("delta").mode("append") \
    .option("mergeSchema", "true") \
    .save(f"Tables/bronze_{table_name}")

# Update watermark control table
new_high_watermark = new_records.agg(F.max(watermark_col)).collect()[0][0]
spark.sql(f"""
    UPDATE platform_services.pipeline_control
    SET watermark_value = '{new_high_watermark}', last_run_timestamp = current_timestamp()
    WHERE source_system = '{source_system}' AND table_name = '{table_name}'
""")
```

---

## Silver Layer: Clean with Accountability

### Design Principles
1. **Document every transformation.** The Silver layer carries a data dictionary, not just a schema.
2. **Quality gates, not quality hopes.** Every Silver table has explicit quality checks before promotion.
3. **SCD Type 2 for slowly changing dimensions.** History is preserved at the Silver layer.

### Standard Transformation Notebook Pattern

```python
# Silver transformation: customer domain example
# Fabric Notebook, PySpark

from pyspark.sql import functions as F
from pyspark.sql.types import *
from delta.tables import DeltaTable
import logging

logger = logging.getLogger(__name__)

# ---------------------------------------------------------
# 1. LOAD BRONZE SOURCE
# ---------------------------------------------------------
bronze_df = spark.read.format("delta").load("Tables/bronze_customers")

# ---------------------------------------------------------
# 2. DATA QUALITY CHECKS (fail fast if critical failures)
# ---------------------------------------------------------
total_count = bronze_df.count()
null_id_count = bronze_df.filter(F.col("customer_id").isNull()).count()
null_id_rate = null_id_count / total_count if total_count > 0 else 0

if null_id_rate > 0.01:  # > 1% null primary keys is a critical failure
    raise ValueError(
        f"CRITICAL: {null_id_rate:.1%} null customer_id values in Bronze. "
        f"Cannot promote to Silver. Investigate source extraction."
    )

logger.info(f"Bronze quality check passed: {null_id_rate:.3%} null IDs ({null_id_count}/{total_count})")

# ---------------------------------------------------------
# 3. TRANSFORMATIONS
# ---------------------------------------------------------
silver_df = (
    bronze_df
    # Standardize email format
    .withColumn("email_normalized", F.lower(F.trim(F.col("email_address"))))
    
    # Standardize phone: strip non-numeric, enforce 10-digit
    .withColumn("phone_normalized",
        F.regexp_replace(F.col("phone_number"), r"[^0-9]", "")
    )
    .withColumn("phone_valid",
        F.when(F.length(F.col("phone_normalized")) == 10, True).otherwise(False)
    )
    
    # Parse and validate dates
    .withColumn("created_date_parsed",
        F.to_date(F.col("created_date_raw"), "yyyy-MM-dd")
    )
    .withColumn("created_date_valid",
        F.col("created_date_parsed").isNotNull()
    )
    
    # Conform country codes to ISO 3166-1 alpha-2
    .withColumn("country_code_iso",
        F.upper(F.trim(F.col("country_code")))
    )
    
    # Add silver audit columns
    .withColumn("_silver_timestamp", F.current_timestamp())
    .withColumn("_silver_version", F.lit("1.0"))
    .withColumn("_source_bronze_ingest_ts", F.col("_ingest_timestamp"))
    
    # Drop Bronze-specific columns not needed in Silver
    .drop("_ingest_timestamp", "_pipeline_run_id", "email_address", 
          "phone_number", "created_date_raw", "country_code")
)

# ---------------------------------------------------------
# 4. QUALITY METRICS (written to monitoring table)
# ---------------------------------------------------------
quality_metrics = {
    "table": "silver_customers",
    "run_timestamp": F.current_timestamp(),
    "total_records": silver_df.count(),
    "phone_valid_rate": silver_df.filter(F.col("phone_valid")).count() / silver_df.count(),
    "date_valid_rate": silver_df.filter(F.col("created_date_valid")).count() / silver_df.count(),
    "email_null_rate": silver_df.filter(F.col("email_normalized").isNull()).count() / silver_df.count()
}

# Write quality metrics to monitoring Lakehouse
spark.createDataFrame([quality_metrics]).write.format("delta").mode("append") \
    .save("Tables/silver_quality_metrics")

# ---------------------------------------------------------
# 5. MERGE INTO SILVER (upsert pattern)
# ---------------------------------------------------------
if DeltaTable.isDeltaTable(spark, "Tables/silver_customers"):
    delta_table = DeltaTable.forPath(spark, "Tables/silver_customers")
    delta_table.alias("target").merge(
        silver_df.alias("source"),
        "target.customer_id = source.customer_id"
    ).whenMatchedUpdateAll() \
     .whenNotMatchedInsertAll() \
     .execute()
else:
    silver_df.write.format("delta").mode("overwrite") \
        .option("overwriteSchema", "true") \
        .save("Tables/silver_customers")

logger.info("Silver promotion complete.")
```

---

## Gold Layer: Optimize for Use

### Design Principles
1. **One Gold table per business question, not per source table.** Gold tables are use-case driven.
2. **Pre-join where semantically stable.** Reduce query complexity for analysts and AI applications.
3. **Document business rules explicitly.** Every Gold measure has a definition in the semantic model.

### Gold Table: Customer 360

The Customer 360 Gold table is a canonical example — it joins customer attributes, transaction history, and engagement signals into a single AI-ready view:

```python
# Gold layer: Customer 360 view
# Fabric Notebook, PySpark

silver_customers = spark.read.format("delta").load("Tables/silver_customers")
silver_transactions = spark.read.format("delta").load("Tables/silver_transactions")
silver_support = spark.read.format("delta").load("Tables/silver_support_cases")
silver_engagement = spark.read.format("delta").load("Tables/silver_engagement_events")

# Transaction aggregates (last 12 months)
transaction_agg = (
    silver_transactions
    .filter(F.col("transaction_date") >= F.add_months(F.current_date(), -12))
    .groupBy("customer_id")
    .agg(
        F.sum("transaction_amount").alias("ltm_revenue"),
        F.count("transaction_id").alias("ltm_transaction_count"),
        F.avg("transaction_amount").alias("ltm_avg_order_value"),
        F.max("transaction_date").alias("last_transaction_date"),
        F.datediff(F.current_date(), F.max("transaction_date")).alias("days_since_last_purchase")
    )
)

# Support case aggregates
support_agg = (
    silver_support
    .filter(F.col("case_open_date") >= F.add_months(F.current_date(), -12))
    .groupBy("customer_id")
    .agg(
        F.count("case_id").alias("ltm_support_cases"),
        F.avg("resolution_days").alias("avg_resolution_days"),
        F.sum(F.when(F.col("csat_score") >= 4, 1).otherwise(0)).alias("positive_csat_count")
    )
)

# Engagement signals
engagement_agg = (
    silver_engagement
    .filter(F.col("event_date") >= F.add_months(F.current_date(), -3))
    .groupBy("customer_id")
    .agg(
        F.countDistinct("session_id").alias("sessions_90d"),
        F.count("event_id").alias("events_90d"),
        F.max("event_date").alias("last_active_date")
    )
)

# Build Customer 360 Gold view
customer_360 = (
    silver_customers
    .join(transaction_agg, on="customer_id", how="left")
    .join(support_agg, on="customer_id", how="left")
    .join(engagement_agg, on="customer_id", how="left")
    
    # Derived signals for AI features
    .withColumn("churn_risk_signal",
        F.when(
            (F.col("days_since_last_purchase") > 90) & 
            (F.col("sessions_90d") < 2), "High"
        ).when(
            (F.col("days_since_last_purchase") > 45) | 
            (F.col("sessions_90d") < 5), "Medium"
        ).otherwise("Low")
    )
    .withColumn("customer_tier",
        F.when(F.col("ltm_revenue") >= 10000, "Enterprise")
        .when(F.col("ltm_revenue") >= 2500, "Growth")
        .when(F.col("ltm_revenue") >= 500, "Standard")
        .otherwise("Emerging")
    )
    .withColumn("_gold_timestamp", F.current_timestamp())
    .withColumn("_gold_version", F.lit("1.0"))
)

# Write to Gold Lakehouse
customer_360.write.format("delta").mode("overwrite") \
    .option("overwriteSchema", "true") \
    .partitionBy("customer_tier") \
    .save("Tables/gold_customer_360")

print(f"Gold Customer 360: {customer_360.count():,} records written.")
print(f"Churn signal distribution:")
customer_360.groupBy("churn_risk_signal").count().show()
```

---

## Pipeline Orchestration

The full medallion pipeline is orchestrated using **Data Factory** in Fabric with sequential phase dependencies:

```
Daily Schedule (2:00 AM)
        │
        ▼
[Bronze Ingest Pipeline]     ← Parallel ingestion across all source systems
        │
        ▼
[Bronze Quality Check]       ← Fail pipeline if critical quality thresholds breached
        │
        ▼
[Silver Transform Pipeline]  ← Sequential transformation per domain
        │
        ▼
[Silver Quality Report]      ← Write metrics; alert if SLA breach
        │
        ▼
[Gold Refresh Pipeline]      ← Rebuild Gold tables from latest Silver
        │
        ▼
[Semantic Model Refresh]     ← Trigger Power BI semantic model refresh
        │
        ▼
[Pipeline Success Notification]
```

Failure at any stage triggers an alert and halts downstream steps. The quality gate between Bronze and Silver is the most important control — it prevents low-quality raw data from propagating into the governed estate.

---

*This architecture is part of Jennifer Kelleman's Microsoft Fabric program portfolio.*
*[AIwithjen.com](https://aiwithjen.com)*
