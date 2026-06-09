[Clinical Trials Scraper](https://apify.com/azureblue/clinical-trials-scraper?fpr=data)

**Search ClinicalTrials.gov by condition and status — returns structured JSON with NCT IDs, phases, sponsors, and enrollment numbers.**

Query the world's largest clinical trial registry with 500,000+ studies. Filter by disease, recruitment status, and result count. No API key required — uses the official ClinicalTrials.gov v2 REST API.

---

## What does this Actor do?

This Actor queries the ClinicalTrials.gov v2 API and returns structured records for each matching trial: NCT identifier, title, condition, trial phase, lead sponsor, enrollment count, start date, and a direct link to the trial page.

---

## Use Cases

### 1. Drug Development Pipeline Intelligence

A biotech analyst tracks all recruiting Phase 3 trials for a specific indication: `condition: "non-small cell lung cancer"`, `status: "recruiting"`. The output feeds a competitive intelligence dashboard that alerts the team when new sponsored trials are announced.

### 2. Patient Recruitment Research

A hospital research coordinator looks for all currently recruiting trials at their institution by searching `condition: "heart failure"`, `status: "recruiting"`, `maxResults: 200`. They cross-reference the NCT IDs with their patient database to identify eligible participants.

### 3. Academic Systematic Review

A medical student writing a thesis on immunotherapy needs all completed Phase 2 and 3 trials: `condition: "checkpoint inhibitor melanoma"`, `status: "completed"`. The structured JSON output (NCT ID, sponsor, enrollment, dates) is imported directly into their reference manager.

---

## Input

| Field | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `condition` | String | ✅ Yes | — | Disease or medical condition to search |
| `status` | Enum | No | `all` | `all`, `recruiting`, `completed`, `not_yet`, `active` |
| `maxResults` | Integer | No | `50` | Maximum results to return (1–10,000) |

### Example Input

```
{
  "condition": "type 2 diabetes insulin resistance",
  "status": "recruiting",
  "maxResults": 100
}
```

---

## Output

```
{
  "nctId": "NCT05123456",
  "title": "Effect of Empagliflozin on Insulin Resistance in Type 2 Diabetes",
  "condition": "Type 2 Diabetes Mellitus; Insulin Resistance",
  "status": "RECRUITING",
  "phase": "PHASE3",
  "sponsor": "Boehringer Ingelheim",
  "startDate": "2023-06",
  "completionDate": "2026-12",
  "enrollmentCount": 450,
  "url": "https://clinicaltrials.gov/study/NCT05123456"
}
```

---

## Pricing

**$0.008 per trial record.**

| Volume | Estimated Cost |
| --- | --- |
| 50 results | ~$0.40 |
| 500 results | ~$4.00 |
| 5,000 results | ~$40.00 |

---

## Technical Details

- **Data source**: ClinicalTrials.gov v2 REST API (official, public)
- **Rate limiting**: 1 request / 2 seconds
- **Retry logic**: 3 retries with exponential backoff
- **Pagination**: automatic via `nextPageToken`
- **Node.js**: v22 LTS