# Data dictionary

`data/sample_awards.csv` and `data/awards_clean.csv` have the same columns. Each row is one contract award for one company.

| Field | Type | Meaning |
|---|---|---|
| `company` | text | Which of the nine companies the award was searched under. |
| `award_id` | text | The contract or order number. Not unique on its own. |
| `award_unique_id` | text | USAspending's unique ID for the award (`generated_internal_id`). |
| `recipient_name` | text | Legal name of the company or subsidiary that received the award, as the government reports it. |
| `recipient_id` | text | USAspending's ID for that recipient. |
| `award_amount` | number | Total dollars on the award over its whole life, not for one year. |
| `start_date` | date | When the award's period of performance begins. |
| `end_date` | date | When the award's period of performance ends. |
| `start_fiscal_year` | integer | Federal fiscal year of `start_date`. Fiscal years begin October 1. |
| `started_before_fy2020` | true/false | True if the award began before fiscal 2020 but was still active during the study window. |
| `awarding_branch` | text | The DoD component that made the award, such as Department of the Navy. |
| `contract_type` | text | Award type: definitive contract, delivery order, purchase order, or BPA call. |
| `description` | text | The government's short description of the work. Missing for 82 awards. |
| `naics_code` | text | Industry code (North American Industry Classification System). Missing for 28 awards. |
| `naics_description` | text | Name of the NAICS code. |
| `psc_code` | text | Product or Service Code: what was bought. |
| `psc_description` | text | Name of the PSC code. |
| `shared_with_other_company` | true/false | True if the same award also appears under another company in the list, as with joint ventures. |
