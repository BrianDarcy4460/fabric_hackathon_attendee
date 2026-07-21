---
layout: page
title: Notebooks
---

# Example Notebooks

These are **reference notebooks** (`.ipynb`) that show one complete path through the
hackathon using a medallion architecture (Bronze → Silver → Gold). Use them as a guide —
you are encouraged to adapt them to your own data and ideas.

> The notebooks were authored in Microsoft Fabric. Import an `.ipynb` into your workspace
> (**Workspace → New → Import notebook**), then attach the appropriate Lakehouse before running.
> They resolve workspace items by name at runtime, so there are no tenant GUIDs to edit.

## Silver — Transform (Goal 2)

| Notebook | What it does |
| --- | --- |
| `1 - Normalize SIS to Silver Lakehouse.ipynb` | Reads the Bronze SIS mirror (Azure SQL mirrored into OneLake), conforms 11 tables to `snake_case`, enforces primary keys, and writes managed Delta dimensions/facts to `SilverLakehouse` (`dbo` schema). |
| `2 - Transform Grad Exams to Silver Lakehouse.ipynb` | Reads the Bronze Graduate Exams mirror (Cosmos), flattens the nested `undergradContext`, explodes `relevantCourses[]`, and writes `dbo.grad_exam_result` and `dbo.grad_exam_relevant_course`. |

## AI — Discover Insights (Goal 3)

| Notebook | What it does |
| --- | --- |
| `3 - Anonymize Course reviews with Foundry AI.ipynb` | Calls an Azure AI Foundry chat model to anonymize/rewrite free-text course reviews (removing identifiers) and writes a de-identified Silver table. Endpoint/key come from a Fabric Variable Library. |
| `4 - Analyze CR with Built-in AI.ipynb` | Uses Fabric's built-in AI functions (`ai.analyze_sentiment`, `ai.summarize`, `ai.classify`, `ai.extract`) over the raw review text to derive sentiment, recommendation, and topic themes into `course_review_signal_ai`. |

## Gold — Model & Serve (Goal 4)

| Notebook | What it does |
| --- | --- |
| `Gold - Business Marts (MLV).ipynb` | Builds the Gold layer as **Materialized Lake Views** in `GoldLakehouse`: four Tier-1 wide marts and six Tier-2 business-question answers, ready for a Direct Lake semantic model and Data Agents. |
