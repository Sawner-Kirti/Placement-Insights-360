# Placement Insights 360 - Campus Placement Analytics (Advanced Excel)

> An interactive Excel dashboard that answers the questions a placement cell actually asks: **Who gets placed, why, at what package, by which recruiters, and which students need help before it is too late?**

![Excel dashboard](docs/excel_dashboard.png)

---

## 1. Business problem
A placement cell tracks hundreds of students across batches and courses, dozens of recruiters and thousands of applications. Leadership wants to:
1. Monitor placement rate, package (CTC) and recruiter performance per batch and course.
2. Find where candidates drop out of the hiring funnel.
3. Check whether interview readiness (DSA practice, CGPA, projects, mocks, internships) really predicts placement.
4. Identify students who need support early.

## 2. Dataset (synthetic, 3 related tables)
| File | Rows | Description |
|---|---|---|
| `data/students.csv` | 600 | Batch, course, city tier, CGPA, DSA problems solved, projects, internship, mock-interview score |
| `data/companies.csv` | 30 | Fictional recruiters with sector, tier (1-3) and HQ city |
| `data/applications.csv` | ~3,100 | Student x company applications, furthest stage reached, offer CTC, accepted flag, dates |

## 3. Workbook guide (`excel/Placement_Insights_360.xlsx`)
About 26,500 live formulas with **0 errors**. Change a cell in `Assumptions` or the batch dropdown on `Dashboard`, and everything recalculates.

| Sheet | What it does |
|---|---|
| `Dashboard` | Batch dropdown, 6 KPI cards, auto-generated insight sentences, 6 charts |
| `Analysis` | Calculation engine: 9 summary tables that feed the dashboard |
| `Students` | Raw attributes plus calculated Readiness Score, Tier, Offers, Placed, CTC, Company |
| `Applications` | One row per application; lookup columns pull Batch, Course, Sector, Tier |
| `Companies` | Recruiter master plus live Applications / Offers / Hires / Avg CTC |
| `Assumptions` | Editable weights, tier thresholds, CTC bands, stage order (blue = input) |

## 4. Excel skills demonstrated
| Skill | Where |
|---|---|
| Two-way lookups (`INDEX` / `MATCH`) across sheets | `Applications` |
| Multi-criteria aggregation (`COUNTIFS`, `SUMIFS`, `AVERAGEIFS`, `MAXIFS`) | `Analysis`, `Companies` |
| Wildcard-criterion trick: one dropdown means "All" or a single batch | `Analysis!B2` |
| Array formula (`MEDIAN(IF(...))`) | Median CTC |
| Top-N without sorting (`LARGE` + `MATCH` + tie-breaker key) | Top 10 recruiters |
| Weighted scoring model driven by editable assumptions | `Students` Readiness Score |
| Approximate-match banding (`LOOKUP`) | Readiness Tier |
| Excel Tables, data validation, frozen panes | all data sheets |
| Conditional formatting (data bars, colour scales, icon sets, rules) | `Students`, `Applications`, `Analysis` |
| Dynamic text insights (`INDEX`/`MATCH` + `TEXT`) | `Dashboard` |
| Native charts, KPI cards, one-page print layout | `Dashboard` |

## 5. Sample findings (from the synthetic data)
* Overall placement rate **64.7%** (388 of 600); average package **10.2 LPA**, median **8.4 LPA**, highest **29.9 LPA**.
* **Readiness predicts outcomes:** placement rate climbs from **29%** (Foundation tier) to **93%** (Elite tier).
* **Internships matter:** 75% of students with an internship were placed vs 59% without.
* **DSA with Java** has the highest placement rate (**76.5%**); **Data Analytics** the lowest (**51.0%**).
* **Funnel:** only 28% of applications reach an offer (876 of 3,143); the biggest leak is the Online Test (32% of applications drop there).
* Tier-1 recruiters hire few (39 hires) but pay about **23.8 LPA** on average, versus 5.9 LPA for Tier-3 firms (188 hires).
* Placement rate by batch: 2024 = 70.6%, 2025 = 61.5%, 2026 = 62.7%.

## 6. Recommendations a placement cell could act on
1. Mentor Foundation and Developing tier students who are still unplaced first.
2. Make mock interviews and an internship or project requirement part of the programme for weaker tiers.
3. Add online test preparation sprints, since that is the largest funnel leak.
4. Target more Tier-1 and Tier-2 analytics recruiters for the Data Analytics cohort.
