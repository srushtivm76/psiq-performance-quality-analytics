# OpsIQ — Operations Performance & Quality Analytics

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458.svg)](https://pandas.pydata.org/)
[![SciPy](https://img.shields.io/badge/SciPy-Statistical%20Analysis-8CA1AF.svg)](https://scipy.org/)
[![SQL](https://img.shields.io/badge/SQL-PostgreSQL%2FANSI-336791.svg)](sql/operations_analysis.sql)
[![Excel](https://img.shields.io/badge/Excel-MIS%20Reporting-217346.svg)](excel/OpsIQ_Analysis.xlsx)
[![Power BI](https://img.shields.io/badge/Power_BI-Executive_Dashboard-F2C811.svg)](dashboard/OpsIQ_Operations_Performance_Dashboard.pbix)
[![Power BI Live Service](https://img.shields.io/badge/Power_BI-Live%20Interactive%20Report-F2C811.svg?logo=powerbi)](https://app.powerbi.com/groups/me/reports/aa8ba15c-7027-4def-a4ea-835980d3a02f/7e01949f56bc2935477d?experience=power-bi)

**Domain**: Trust & Safety / Content Moderation / Operations Analytics  
**Target Role Alignment**: Data Analyst Project Intern — Training & Quality (ByteDance / Social Media Operations)  
**Dataset Size**: 50,000 Content Moderation Records  


---

## 📊 Executive Power BI Dashboard Preview

> 🌐 **Live Interactive Report**: Access the published Power BI report directly on Power BI Service:  
> 👉 **[Click Here to Open Live Interactive OpsIQ Dashboard](https://app.powerbi.com/groups/me/reports/aa8ba15c-7027-4def-a4ea-835980d3a02f/7e01949f56bc2935477d?experience=power-bi)**

### Page 1 — Operations Overview
![Page 1 — Operations Overview](screenshots/Page%201.png)

### Page 2 — Training & Quality Analytics
![Page 2 — Training & Quality Analytics](screenshots/Page%202.png)

### Page 3 — Operational Efficiency & Outlier Analysis
![Page 3 — Operational Efficiency & Outlier Analysis](screenshots/Page%203.png)

---

## 1. Executive Summary & Project Overview

**OpsIQ** is an end-to-end operations analytics project built around a high-volume social media content moderation workflow. Starting with a synthetic social media toxic content dataset, OpsIQ constructs a realistic operational data layer simulating 50,000 day-to-day moderation tasks across global teams, platforms, and content formats.

### Core Business Question
> **How can statistical analysis and operational reporting be used to identify quality problems, evaluate the impact of moderator training, detect performance trends, and deliver actionable recommendations to operations management?**

```
Social Media Toxic Comment Dataset (49,998 rows)
                │
                ▼
       Data Understanding (01_data_understanding.ipynb)
                │
                ▼
          Data Cleaning (02_data_cleaning.ipynb)
                │
                ▼
      Operational Data Generation (generate_operations_data.py)
                │
                ▼
      50K Moderation Operational Records (moderation_operations.csv)
                │
       ┌────────┼─────────┐
       ▼        ▼         ▼
    Python     SQL      Excel
   (SciPy)   (ANSI)  (openpyxl)
       │        │         │
       └────────┼─────────┘
                ▼
      Statistical Analysis (03_statistical_analysis.ipynb)
                │
                ▼
     Power BI Dashboard (OpsIQ.pbix / Screenshots)
                │
                ▼
      Management Insights & Actionable Recommendations
```

---

## 2. Dataset Architecture & Schema

The dataset combines moderation content labels (`toxic`, `severe_toxic`, `obscene`, `insult`, `threat`, `hate_speech`) with a 26-column synthetic operational layer.

| Field Name | Data Type | Description / Operational Purpose |
|---|---|---|
| `task_id` | String | Unique moderation task identifier (`TSK_000001`) |
| `comment_id` | String | Source comment reference ID |
| `moderator_id` | String | Assigned moderator ID (`MOD_101` to `MOD_250`) |
| `team` | String | Operational team (`Team Alpha` - `Team Epsilon`) |
| `region` | String | Geographic region (`NA`, `EMEA`, `APAC`, `LATAM`) |
| `platform` | String | Moderated platform (`TikTok`, `CapCut`, `Douyin`, `LiveStream`) |
| `content_type` | String | Format (`Short Video Caption`, `Long Form Comment`, `Image Text Overlay`, etc.) |
| `language` | String | Content language (`English`, `Spanish`, `Portuguese`, `Bahasa`, `Tagalog`, `Japanese`) |
| `timestamp` | Datetime | Execution timestamp over 6 months (Jan 2026 - Jun 2026) |
| `date` | Date | Calendar date (`YYYY-MM-DD`) |
| `week` | String | Calendar week identifier (`YYYY-W01`) |
| `month` | Integer | Calendar month integer (`1` to `6`) |
| `month_name` | String | Abbreviated month name (`Jan` to `Jun`) |
| `label` | Categorical | Toxic content classification label |
| `training_status` | Categorical | Moderator status (`Trained` vs `Untrained`) |
| `training_hours` | Numeric | Total training hours logged (0 to 40 hours) |
| `tasks_completed` | Integer | Total tasks completed per shift (80 to 380) |
| `review_time_sec` | Numeric | Review duration in seconds (10 to 180s) |
| `quality_score` | Numeric | Quality score (0.00 to 100.00 scale) |
| `quality_category` | Categorical | Quality tier (`Excellent`, `Good`, `Needs Improvement`, `Poor`) |
| `productivity_tasks_per_hour` | Numeric | Productivity KPI (`tasks_completed / 8.0`) |
| `error_flag` | Binary | Binary error indicator (`1` = Error, `0` = No Error) |
| `error_type` | Categorical | Error taxonomy (`Policy Misinterpretation`, `Misclassification`, `Missed Context`, `False Positive`) |
| `escalated` | Binary | Escalation indicator (`1` = Escalated, `0` = Standard) |
| `comment_text` | String | Text content reviewed |
| `text_length` | Integer | Character length of text |
| `word_count` | Integer | Word count of comment text |

---

## 3. Key Statistical Analysis & Hypothesis Testing

### 3.1 Descriptive Statistics
Operational summary across 49,998 tasks:
- **Quality Score**: Mean = `85.58`, Median = `86.42`, Std Dev = `7.81`
- **Review Duration**: Mean = `35.2 sec`, Median = `33.4 sec`, IQR = `14.8 sec`
- **Productivity**: Mean = `26.2 tasks/hr`, Median = `26.1 tasks/hr`
- **Error Rate**: Overall = `22.44%` (Trained: `17.51%`, Untrained: `32.94%`)

### 3.2 Hypothesis Testing — Welch's Two-Sample t-Test
To evaluate whether moderator training produces a statistically significant improvement in quality:

$$\begin{aligned}
H_0 &: \mu_{\text{trained}} - \mu_{\text{untrained}} = 0 \quad \text{(Training has no effect on quality)} \\
H_1 &: \mu_{\text{trained}} - \mu_{\text{untrained}} \neq 0 \quad \text{(Training significantly improves quality)}
\end{aligned}$$

Using Welch's t-test (unequal variances assumed):
- **Trained Quality Mean**: `88.23`
- **Untrained Quality Mean**: `79.92`
- **Difference ($\Delta$)**: `+8.31` quality points
- **t-Statistic**: `108.45`
- **p-Value**: `< 0.0001` (Reject $H_0$)

**Business Interpretation**: There is statistically significant evidence ($p < 0.001$) that trained moderators achieve higher quality scores than untrained moderators.

### 3.3 Correlation Analysis
Evaluating training exposure against moderation accuracy:
- Pearson Correlation Coefficient ($r$) between `training_hours` and `quality_score`: **$r = +0.52$** (Moderate positive relationship).
- Spearman Correlation Coefficient ($\rho$) between `review_time_sec` and `quality_score`: **$\rho = +0.28$** (Longer review duration weakly correlates with higher quality).

### 3.4 Outlier Detection via IQR Method
Detecting operational review duration anomalies:

$$\begin{aligned}
Q_1 &= 27.2\text{s}, \quad Q_3 = 42.0\text{s}, \quad \text{IQR} = 14.8\text{s} \\
\text{Upper Outlier Threshold} &= Q_3 + 1.5 \times \text{IQR} = 42.0 + 1.5(14.8) = \mathbf{64.2\text{s}}
\end{aligned}$$

Tasks exceeding `64.2 seconds` are flagged for workflow bottleneck inspection.

---

## 4. SQL Analytics Suite

The SQL suite in [`sql/operations_analysis.sql`](file:///o:/Data%20Analysis%20Projects/OpsIQ%20%E2%80%94%20Operations%20Performance%20&%20Quality%20Analytics/sql/operations_analysis.sql) translates operational business questions into ANSI SQL queries.

```sql
-- Team & Region Operational Performance Aggregation
SELECT 
    team,
    region,
    COUNT(task_id) AS total_tasks,
    ROUND(AVG(quality_score), 2) AS avg_quality,
    ROUND(AVG(error_flag) * 100.0, 2) AS error_rate_pct,
    ROUND(AVG(productivity_tasks_per_hour), 2) AS avg_productivity,
    ROUND(AVG(review_time_sec), 1) AS avg_review_time_sec
FROM moderation_operations
GROUP BY team, region
ORDER BY avg_quality ASC;
```

---

## 5. Excel MIS Reporting

The Excel workbook in [`excel/OpsIQ_Analysis.xlsx`](file:///o:/Data%20Analysis%20Projects/OpsIQ%20%E2%80%94%20Operations%20Performance%20&%20Quality%20Analytics/excel/OpsIQ_Analysis.xlsx) (generated via `src/build_excel_mis.py`) consists of 4 automated executive sheets:

1. **Executive Summary**: High-level KPI cards, category breakdown, weighted formula totals (`SUM`, `AVERAGE`).
2. **Team Performance**: Cross-tabular analysis of teams and regions with conditional formatting.
3. **Training Analysis**: Training status breakdown and training exposure hour tiers (`< 10 hrs`, `10-19 hrs`, `20-29 hrs`, `30+ hrs`).
4. **Daily MIS**: Time-series daily tracking table with daily averages, task volumes, error rates, and escalations.

---

## 6. Power BI Executive Management Dashboard

> 🌐 **Live Interactive Report**: Access the published Power BI report directly on Power BI Service:  
> 👉 **[Click Here to Open Live Interactive OpsIQ Dashboard](https://app.powerbi.com/groups/me/reports/aa8ba15c-7027-4def-a4ea-835980d3a02f/7e01949f56bc2935477d?experience=power-bi)**

The executive dashboard layout comprises 3 interactive, cross-filtered pages designed for senior operations leadership, quality managers, and workflow leads:

### Page 1 — Operations Overview
![Page 1 — Power BI Operations Overview](screenshots/Page%201.png)
![Operations Overview Visuals](screenshots/overview.png)

* **Objective**: Provides an executive macro view of operational performance, throughput, quality scores, and review times across global teams and content platforms.
* **Key Visuals & KPIs**:
  * **Executive KPI Cards**: Total Moderation Tasks (`50.00K`), Average Quality Score (`85.58`), Average Review Time (`35.2 sec`), Escalation Rate (`5.10%`).
  * **Time-Series Volume & Quality Trends**: Monthly and daily task volume tracking vs. average quality score to identify operational surge periods.
  * **Team & Region Breakdown**: Cross-tabular analysis comparing Teams Alpha through Epsilon across NA, EMEA, APAC, and LATAM regions.
  * **Platform & Content Type Metrics**: Performance segmentation across TikTok, CapCut, Douyin, and LiveStream formats.

---

### Page 2 — Training & Quality Analytics
![Page 2 — Power BI Training & Quality Analytics](screenshots/Page%202.png)
![Training & Quality Visuals](screenshots/training_quality.png)

* **Objective**: Evaluates the quantitative ROI of moderator training exposure on quality scores, error rate reduction, and error taxonomy.
* **Key Visuals & KPIs**:
  * **Training Status Comparison**: Direct KPI comparison between **Trained** (Quality: `88.23`, Error Rate: `17.51%`) and **Untrained** staff (Quality: `79.92`, Error Rate: `32.94%`).
  * **Training Hour Exposure Tiers**: Quality score distribution across training duration tiers (`<10 hrs`, `10-19 hrs`, `20-29 hrs`, `30+ hrs`), confirming quality stabilization at `25+ hours`.
  * **Error Taxonomy Root-Cause Breakdown**: Categorization of operational errors showing `Policy Misinterpretation` as the primary error driver (35%), followed by `Misclassification` and `Missed Context`.
  * **Interactive Slicers**: Filterable by Team, Platform, Content Category, and Language.

---

### Page 3 — Operational Efficiency & Outlier Analysis
![Page 3 — Power BI Operational Efficiency & Outlier Analysis](screenshots/Page%203.png)
![Operational Efficiency Visuals](screenshots/efficiency.png)

* **Objective**: Analyzes reviewer throughput, review duration distributions, productivity vs. quality trade-offs, and detects workflow bottlenecks via IQR outlier thresholding.
* **Key Visuals & KPIs**:
  * **Review Duration Latency Distribution**: Histogram and scatter analysis highlighting tasks exceeding the `64.2-second` upper outlier threshold ($Q_3 + 1.5 \times \text{IQR}$).
  * **Productivity vs. Quality Trade-Off**: Scatter analysis comparing tasks/hour against error rate, revealing elevated error spikes when review times fall below `18 seconds`.
  * **Escalation Audit Matrix**: Breakdown of escalated tasks by content severity (`threat`, `severe_toxic`) and platform for supervisor priority review.
  * **Supervisor Action Table**: Flagged high-risk moderation tasks requiring immediate QA review.

---

## 7. Executive Insights & Actionable Recommendations

### Key Management Insights
1. **Training Impact**: Trained moderators achieve an average quality score of `88.23` compared to `79.92` for untrained moderators ($p < 0.001$), reducing error rates from `32.94%` to `17.51%`.
2. **Exposure Threshold**: Training hours exhibit a positive correlation ($r = 0.52$) with quality score, showing optimal quality stabilization beyond `25 hours` of exposure.
3. **Productivity vs. Quality Trade-Off**: High-productivity tiers (>35 tasks/hr) exhibit elevated error rates when review duration falls below `18 seconds`.
4. **Policy Misinterpretation**: Policy misinterpretation accounts for `35%` of total errors, representing the single largest root cause of moderation mistakes.

### Actionable Recommendations
1. **Mandatory Onboarding Gate**: Require at least `20 hours` of structured policy training prior to assigning live moderation tasks to eliminate the `32.94%` error rate observed in untrained staff.
2. **Targeted Refresher Modules**: Implement micro-training focused on `Policy Misinterpretation` and high-severity content categories (`threat`, `severe_toxic`).
3. **Dual SLA Monitoring**: Evaluate moderators using a combined metric (Quality Score $\ge 85$ + Error Rate $\le 15\%$) rather than throughput alone.
4. **Automated Anomaly Audit**: Flag review times exceeding `64.2 seconds` for supervisor review to identify complex edge cases and UI workflow latency.

---

## 8. Alignment with ByteDance Data Analyst Job Description

| ByteDance JD Requirement | OpsIQ Project Demonstration |
|---|---|
| **Timely reporting & MIS frameworks** | Built automated daily/weekly/monthly Excel MIS report and Power BI executive pages. |
| **Analyzing results using statistical techniques** | Applied Welch's t-test, hypothesis testing, correlation analysis ($r=0.52$), and IQR outlier detection. |
| **Identifying trends & patterns** | Analyzed time-series trends across 6 months of daily moderation task volume and escalations. |
| **Data pipelines & maintaining datasets** | Created raw $\rightarrow$ clean $\rightarrow$ operational synthetic data transformation pipeline (50K records). |
| **Advanced Excel & SQL proficiency** | Authored multi-tab formatted Excel workbooks with formulas and 9 comprehensive ANSI SQL queries. |
| **Actionable business recommendations** | Delivered 4 executive recommendations for Training & Quality operations management. |

---

## 9. Project Repository Structure

```
OpsIQ/
│
├── data/
│   ├── raw/
│   │   └── toxic_comments_50000.csv
│   └── processed/
│       ├── toxic_comments_clean.csv
│       └── moderation_operations.csv
│
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_cleaning.ipynb
│   └── 03_statistical_analysis.ipynb
│
├── src/
│   ├── data_utils.py
│   ├── generate_synthetic_ops_data.py
│   ├── generate_operations_data.py
│   ├── build_excel_mis.py
│   ├── generate_dashboard_images.py
│   └── execute_notebooks.py
│
├── sql/
│   └── operations_analysis.sql
│
├── excel/
│   └── OpsIQ_Analysis.xlsx
│
├── dashboard/
│   └── OpsIQ_Operations_Performance_Dashboard.pbix
│
├── screenshots/
│   ├── Page 1.png
│   ├── Page 2.png
│   ├── Page 3.png
│   ├── overview.png
│   ├── training_quality.png
│   └── efficiency.png
│
├── requirements.txt
└── README.md
```

---

## 10. Reproduction & Setup Instructions

### Prerequisites
- Python 3.10+
- Virtual environment (`.venv`)

### Installation & Execution
```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Generate synthetic operational dataset (50,000 records)
python src/generate_operations_data.py

# 3. Execute Jupyter Notebooks
python src/execute_notebooks.py

# 4. Generate Excel MIS Report
python src/build_excel_mis.py

# 5. Render Dashboard Screenshots
python src/generate_dashboard_images.py
```

---

## 11. Interview Guide & Elevator Pitch

### 30-Second Interview Response
> *"OpsIQ is an operations analytics project focused on content moderation performance and quality. Starting with a 50,000-record toxic comment dataset, I engineered a synthetic operational layer containing moderator attributes, training exposure, quality scores, productivity, review times, error classifications, and escalations. I applied statistical methods including Welch's t-test and correlation analysis in Python to evaluate the ROI of moderator training, authored ANSI SQL queries to model team SLAs, constructed an automated Excel MIS report, and designed a 3-page Power BI executive dashboard with actionable recommendations for operations management."*
