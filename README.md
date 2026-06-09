[Clinical Trials Scraper](https://apify.com/copious_atoll/clinical-trials-scraper?fpr=data)

# Clinical Trials Scraper

Extract clinical trial data from ClinicalTrials.gov, the world's largest registry of clinical studies. Search by condition, drug, sponsor, or keyword to get trial status, phases, enrollment numbers, eligibility criteria, and sponsor details. Powered by the free NIH ClinicalTrials.gov API v2 — no proxy or authentication needed.

> **Disclaimer:** This actor is unofficial and is not affiliated with, sponsored by, or endorsed by the National Institutes of Health (NIH) or the National Library of Medicine (NLM).

## What clinical trial data can you extract?

This actor wraps the free ClinicalTrials.gov API v2 to extract structured study data including:

- **Trial identification** — NCT ID, titles, sponsor name and class (industry, NIH, academic)
- **Status and dates** — overall status (recruiting, completed, etc.), start and completion dates
- **Study design** — phases (1-4), study type (interventional, observational), enrollment count
- **Conditions and interventions** — disease conditions targeted, drug and treatment names
- **Eligibility** — age range, sex, inclusion/exclusion criteria
- **FDA regulation** — whether the study involves FDA-regulated drugs or devices

## Input parameters

| Parameter | Type | Description |
| --- | --- | --- |
| Search Term | string | General keyword search (e.g., "ozempic", "breast cancer") |
| Condition | string | Filter by disease/condition (e.g., "diabetes", "lung cancer") |
| Intervention | string | Filter by drug/treatment (e.g., "pembrolizumab") |
| Trial Status | select | ALL, RECRUITING, COMPLETED, ACTIVE_NOT_RECRUITING, NOT_YET_RECRUITING |
| Max Results | integer | Maximum trials to return (1–1,000, default 50) |

## Output example

Each trial record contains:

```
{
    "nctId": "NCT04564846",
    "briefTitle": "A Study to Evaluate the Effect of ORMD-0801 in Patients With Type 2 Diabetes",
    "officialTitle": "A Randomized, Double Blind, Phase 2b Study...",
    "overallStatus": "COMPLETED",
    "startDate": "2020-11-23",
    "completionDate": "2022-06-07",
    "sponsor": "Oramed, Ltd.",
    "sponsorClass": "INDUSTRY",
    "conditions": ["Diabetes Mellitus, Type 2"],
    "interventions": ["ORMD-0801", "Placebo"],
    "phases": ["PHASE2"],
    "enrollmentCount": 40,
    "enrollmentType": "ACTUAL",
    "studyType": "INTERVENTIONAL",
    "isFdaRegulatedDrug": true,
    "source": "ClinicalTrials.gov",
    "sourceUrl": "https://clinicaltrials.gov/study/NCT04564846"
}
```

## How much does it cost to scrape clinical trials data?

This actor uses **pay-per-event pricing**. You pay per trial record returned.

- **$0.00005 per actor start** (Apify default)
- **Per-result charge** based on the number of trials extracted
- **No proxy costs** — the ClinicalTrials.gov API is free and public

A typical search returns 50 trials at minimal cost. Broad searches (e.g., "cancer") may return thousands of results.

**Tip:** Use specific conditions, interventions, or status filters to narrow results and control costs.

## Who uses clinical trials data?

- **Pharmaceutical companies** — monitor competitor pipelines, track trials for similar drugs and indications
- **Biotech investors** — identify promising drug candidates, track trial phases and enrollment progress
- **Clinical researchers** — find relevant studies, analyze trial design patterns, identify collaboration opportunities
- **Patient advocacy groups** — help patients find recruiting trials for specific conditions
- **Medical journalists** — report on drug development progress, clinical trial trends, and regulatory milestones
- **Regulatory consultants** — track FDA-regulated studies, analyze trial endpoints and completion rates

## Tips for best results

- **Search broadly first** with a simple keyword, then add condition/intervention filters to narrow down.
- **NCT IDs** are unique identifiers — use them to track specific trials across multiple runs.
- **Eligibility criteria** are truncated to 500 characters. Visit the sourceUrl for full criteria.
- **Phase codes**: PHASE1, PHASE2, PHASE3, PHASE4, EARLY_PHASE1, NA (not applicable for observational studies).
- **Enrollment count** shows planned or actual enrollment depending on enrollmentType field.

## Integrations

Export your data as JSON, CSV, or Excel. Schedule weekly runs to monitor trial status changes. Use webhooks to get alerts when new trials match your criteria.

This actor works as an **MCP server** — AI agents can discover and use it to access clinical trials data programmatically.