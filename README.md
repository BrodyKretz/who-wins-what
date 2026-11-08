# Who Wins What: Profiling Defense Contractors in DoD Contract Data

INFO 4617 Web Data Science final project, Brody Kretz.

## Question

Across Department of Defense contract awards from fiscal 2020 through fiscal 2026, how do the biggest defense contractors differ in what they get paid for, and how dependent is each one on a single category of work or a single branch of the military?

## Companies

Lockheed Martin, RTX, Boeing, General Dynamics, Northrop Grumman, Palantir, Anduril, Shield AI, and Scale AI.

## Files

- `01_collect.ipynb` pulls award records from the USAspending API.
- `02_clean.ipynb` turns the raw records into a tidy dataset.
- `data_dictionary.md` explains every field in the cleaned data.
- `data/sample_awards.csv` is a sample of the cleaned data: the ten largest awards for each company.

## Data

**Source.** The [USAspending API](https://api.usaspending.gov/), the federal government's public record of spending under the DATA Act, using `POST /api/v2/search/spending_by_award/`. Requests send a User-Agent with my school email and pause one second between calls, and each response is saved to disk so nothing is pulled twice.

**Collected.** November 8, 2026.

**Scope.** Department of Defense contract awards (types A through D) active from fiscal 2020 through fiscal 2026, meaning October 1, 2019 through September 30, 2026. Each company is searched by its legal names, one fiscal year at a time.

**Records.** 18,145 rows came back from the API. Removing awards returned in more than one fiscal year leaves **5,070 awards** in the cleaned dataset.

**Limits.**
- The API stops at 10,000 records per search and the largest companies have far more. It lists 453,055 company-year award records for these nine companies, so I kept each company's 500 largest awards by dollars per fiscal year. Palantir, Anduril, Shield AI, and Scale AI were under that limit and are complete. The five primes are not, and their smallest awards are missing.
- `award_amount` is an award's lifetime total, so it can't be split by year. 2,381 awards started before fiscal 2020 and are flagged with `started_before_fy2020`.
- DoD contract data is published on about a 90-day delay, so the end of fiscal 2026 is incomplete.
- Company matches come from name searches. Subsidiaries and joint ventures are included when the API links them to a searched name, and the 28 rows for awards shared between two companies are flagged.
- The proposal's defense.gov announcement scrape is deferred. It isn't part of this dataset.

**Left out of the repo.** The full raw responses (`data/raw/`, about 28 MB) and the full cleaned file (`data/awards_clean.csv`) are not committed, because of their size and because this stage only needs a small sample. Terms of service and personal information aren't the reason: the data is public by law and covers a fixed list of large companies. Running `01_collect.ipynb` and then `02_clean.ipynb` rebuilds both.
