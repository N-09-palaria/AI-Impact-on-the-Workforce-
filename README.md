
# AI Impact on the Workforce 2020–2026

**Which job roles AI is most likely to displace — and which will thrive**

[![Tableau](https://img.shields.io/badge/Tableau-E97627?style=flat-square&logo=tableau&logoColor=white)](https://public.tableau.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white)](https://postgresql.org)
[![Figma](https://img.shields.io/badge/Figma-F24E1E?style=flat-square&logo=figma&logoColor=white)](https://figma.com)
[![Excel](https://img.shields.io/badge/Excel-217346?style=flat-square&logo=microsoftexcel&logoColor=white)]()

---

## What this project is about

This project analyses how AI is reshaping job roles between 2020 and 2026 — looking at automation risk, salary impact, and reskilling pressure across 10 occupations.

Built as a complete analytics pipeline: raw CSV → SQL analysis → Tableau dashboard.

---

## Dashboard

> 🔗 [View on Tableau Public →](https://public.tableau.com/app/profile/nikita.palaria/viz/aiworkfoce/aiimpactonworkforce)


![Dashboard Preview](https://github.com/N-09-palaria/AI-Impact-on-the-Workforce-/blob/41fecc57f4956c2ccf580b1be65a16fec8369952/ai%20impact%20on%20workforce%20.png)

---

## Key Findings

| Finding | Number |
|---------|--------|
| Truck Driver automation risk | **60.7%** — highest of all roles |
| Software Engineer automation risk | **34.9%** — lowest of all roles |
| Gap between most and least exposed | **26 percentage points** |
| High Risk workers in dataset | **2,369** (15.8%) |
| Safe Zone workers | **2,194** (14.6%) |
| Annual wage gap (growing vs declining) | **$14,288** per year |
| Reskilling pressure gap | High Risk **49.0** vs Safe Zone **26.9** out of 100 |

---

## Tools Used

| Tool | What I used it for |
|------|--------------------|
| **PostgreSQL** | Data loading, cleaning, 5 analysis queries |
| **Tableau Public** | 9-chart dashboard with dark editorial theme |
| **Figma** | Dashboard wireframe and layout planning |
| **Excel** | Initial data profiling and column inspection |

---

## Dashboard Charts

```
Row 1 — KPI tiles:   46.18% avg risk · 2,369 high risk · 2,194 safe · 49.38% declining pay
Row 2 — Treemap (automation risk by role) + Progress bars (wage gap)
Row 3 — Scatter plot (risk vs reskilling) + Stacked bars (scale of exposure)
Row 4 — Bar charts: highest risk roles vs lowest risk roles
Row 5 — Heatmap: skill gap index by industry and job role
```

---

## Dataset

- **Source:** [Kaggle — algozee/future-of-work-in-the-age-of-ai-20202026](https://www.kaggle.com/datasets/algozee/future-of-work-in-the-age-of-ai-20202026)
- **Size:** 15,000 rows · 23 columns
- **Coverage:** 10 job roles · 8 industries · 9 countries · 2020–2026

> **Note:** This is a synthetic dataset. Industry and country-level patterns are randomly distributed and do not reflect real economic data. Job-role-level patterns show genuine signal and are the focus of this analysis.

---

## SQL Queries

<details>
<summary>Automation risk by job role</summary>

```sql
SELECT
  job_role,
  ROUND(AVG(automation_risk_percent), 2) AS avg_risk,
  ROUND(AVG(reskilling_urgency_score), 2) AS avg_reskilling,
  COUNT(*) AS workers
FROM ai_workforce
GROUP BY job_role
ORDER BY avg_risk DESC;
```

</details>

<details>
<summary>Wage gap after AI disruption</summary>

```sql
SELECT
  salary_direction,
  ROUND(AVG(salary_after_usd), 0) AS avg_salary_after,
  COUNT(*) AS workers
FROM ai_workforce
GROUP BY salary_direction
ORDER BY avg_salary_after DESC;
```

</details>

<details>
<summary>Reskilling urgency by risk zone</summary>

```sql
SELECT
  safe_zone_flag,
  ROUND(AVG(reskilling_urgency_score), 1) AS avg_urgency,
  ROUND(AVG(automation_risk_percent), 1) AS avg_risk,
  COUNT(*) AS workers
FROM ai_workforce
GROUP BY safe_zone_flag
ORDER BY avg_urgency DESC;
```

</details>

---

## How to Run

```bash
# 1. Download the dataset from Kaggle (link above)

# 2. Load into PostgreSQL
\i sql/01_create_table.sql
\COPY ai_workforce FROM 'ai_workforce.csv' DELIMITER ',' CSV HEADER;

# 3. Run analysis queries
\i sql/02_analysis_queries.sql

# 4. Open Tableau → Connect to Text File → ai_workforce.csv
```

---

## Files in this Repo

```
├── sql/
│   ├── 01_create_table.sql
│   └── 02_analysis_queries.sql
├── dashboard/
│   └── dashboard_full.png
├── data/
│   └── dataset_source.txt
└── README.md
```

---

## About

**Nikita Palaria** — MBA, Finance & Business Analytics (Galgotias University, 2025)

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nikita-palaria-43926732a/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/N-09-palaria)
[![Email](https://img.shields.io/badge/Gmail-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:nikitapalaria@gmail.com)
