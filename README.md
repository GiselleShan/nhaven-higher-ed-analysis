# New Haven Higher Education Landscape — Enrollment, Retention & Outcomes Analysis

## Overview

This project is a work sample prepared for the Statistical Data Analyst position at Yale's Office of Institutional Research (OIR). Using publicly available IPEDS data, it analyzes enrollment, retention, and graduation rate trends across four New Haven-area institutions from 2013 to 2023. The project covers the full analytical pipeline: data cleaning, missing-value diagnosis, and visualization.

## Data Source

Data was sourced from the IPEDS Data Center, covering the following four New Haven-area institutions over 2013–2023 (odd years, aligned with IPEDS cohort reporting cycles):

| Institution | UnitID |
|---|---|
| Yale University | 130794 |
| Quinnipiac University | 130226 |
| Southern Connecticut State University | 130493 |
| University of New Haven | 129941 |

Metrics included:
- Full-time / part-time undergraduate enrollment
- Full-time / part-time retention rate
- 4-year / 6-year graduation rate

## Methodology

**Data Cleaning**
- Standardized column names: renamed IPEDS' long, code-heavy export headers (e.g., `"4-year Graduation rate - bachelor's degree within 100% of normal time (GR200_23_RV)"`) into concise snake_case labels (e.g., `grad_rate_4yr_2023`)
- Reshaped wide to long format: used `pd.wide_to_long()` to convert the data from one row per institution (with years spread across column names) into one row per institution-year, making year an independent, analyzable variable

**Missing Value Handling**

During cleaning, Yale's part-time retention rate was found to be missing across all six years (2013–2023). Rather than dropping or imputing these values, I cross-checked the corresponding part-time enrollment counts and found they ranged from single digits to the low twenties — consistent with IPEDS' common practice of suppressing rates calculated from very small sample sizes.

A separate missing value was also found for Quinnipiac in 2021, where the corresponding part-time enrollment was 313 — not a small sample. This gap was treated as a distinct case with an unclear cause, rather than being explained away with the same small-sample reasoning applied to Yale.

In an institutional research context, imputing missing retention data with a mean or interpolation would effectively fabricate enrollment behavior that never occurred — a risk in reports intended for decision-makers. This project therefore preserves missing values as NaN, with data limitations noted explicitly in the accompanying charts and text, rather than presenting numbers that appear complete but are not.

**Visualization**

Four charts were designed around four core questions:

| Chart | Content | Question Answered |
|---|---|---|
| Chart 1 | Full-time enrollment trends (line chart, 4 institutions) | How has enrollment scale changed over the decade at each institution? |
| Chart 2 | Retention rate trends (FT/PT subplots) | Is first-year retention improving or declining? |
| Chart 3 | 6-year graduation rate trends (line chart) | How has long-term graduation performance evolved? |
| Chart 4 | 2023 cross-institution snapshot (grouped bar chart) | Where does each institution stand relative to the others in the most recent year? |

## Key Findings

**Enrollment Trends**
- Yale is the only institution with sustained positive growth, rising from roughly 5,424 students in 2013 to 6,805 in 2023
- Quinnipiac grew until 2017, then entered a decline, falling to roughly 6,070 by 2023
- Southern Connecticut State University (SCSU) shows a clear downward trend, with the steepest decline after 2019 (from roughly 6,814 to 5,392)
- University of New Haven (UNH) remained flat throughout, staying within a 4,400–4,800 range with no clear trend

**Retention Rate Patterns**
- Full-time retention is relatively stable across all four institutions, consistently in the 75%–99% range
- Part-time retention is far more volatile than full-time, with all four institutions experiencing sharp declines (some years near 0%) — but none shows a purely monotonic decline. SCSU and UNH both show signs of recovery in 2021–2023, while Quinnipiac remains at a low point (0%) as of 2023
- This contrast between stable full-time retention and volatile part-time retention may reflect statistical fragility from small part-time sample sizes, genuine differences in student behavior, or both — worth further investigation

**Graduation Rate Trends and Institutional Gaps**
- Yale leads by a wide margin, with 6-year graduation rates holding steady at 97%–98%
- Quinnipiac ranks second, in the 69%–80% range
- UNH and SCSU are both substantially lower, though both show improvement: UNH rose from 53% to 66% (+13 points), while SCSU rose from 44% to 52% (+8 points) — UNH shows the most pronounced improvement of the four institutions


## How to Run

1. Clone this repository
2. Create and activate a virtual environment
3. Install dependencies: pip install -r requirements.txt

4. Open and run the following notebooks in order:
   - `notebooks/01_data_cleaning.ipynb`
   - `notebooks/02_analysis.ipynb`

## Author

Giselle Shan
www.linkedin.com/in/giselleshan




