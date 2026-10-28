# Fabric Notebooks: AI Readiness on Microsoft Fabric

This folder contains two example notebooks for an enterprise data modernization program. They are intended for Microsoft Fabric's Spark runtime; review the configuration and dependencies before running them in a workspace.

## Notebooks in This Folder

| Notebook | Purpose | When to Run |
|---|---|---|
| `01_data_quality_assessment.ipynb` | Scans Bronze tables and produces a data quality report by domain | After each Bronze ingestion cycle |
| `02_ai_readiness_scorecard.ipynb` | Scores each data domain against AI readiness criteria and produces an executive-ready scorecard | Monthly, or before major AI program milestones |

## Running These Notebooks in Microsoft Fabric

1. Open your Microsoft Fabric workspace
2. Create a new Notebook item
3. Paste the notebook content or import the `.ipynb` file
4. Attach to your Lakehouse using the Explorer panel (left sidebar)
5. Run all cells in sequence

Both notebooks write output to Delta tables in the attached Lakehouse. Output tables:
- `Tables/dq_assessment_results` — Data quality scores by domain and table
- `Tables/ai_readiness_scores` — AI readiness scorecard by domain

## How These Notebooks Fit the Program Narrative

These notebooks serve a dual purpose:

**Technical:** They are the quality gate between the Bronze and Silver layers, and the evidence layer for the AI readiness executive briefings.

**Communication:** Executive updates can use the results to explain the current baseline, identify gaps, and agree on next steps. Include the assessment date, definitions, and limitations alongside the scores.

The notebook is the engine. The output is the narrative.
