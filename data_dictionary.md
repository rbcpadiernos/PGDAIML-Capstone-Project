\# Data Dictionary    
\*\*Veterinary Licensure Prediction Dataset\*\*

\---

\#\# 1\. Student Profile Variables

| Variable Name | Type | Description | Allowed Values | Notes |  
|---|---|---|---|---|  
| Student ID | Int64 | Unique identifier assigned to each student | Unique Integer value | Primary key, not used for modeling |  
| Gender | Category | Student gender | Male, Female | Needs standardization (e.g., 'male' → 'Male') |  
| Type of Examinee | Category | Examinee classification | First Taker, Repeater | Potentially strong predictor |

\---

\#\# 2\. First Attempt / Baseline Scores

| Variable Name | Type | Description | Allowed Values | Notes |  
|---|---|---|---|---|  
| Pre-assessment 2025 | Float | Initial diagnostic exam score | 0–100 | Baseline readiness |  
| Anatomy | Float | First Anatomy mock exam score | 0–100 | |  
| Physiology | Float | First Physiology mock exam score | 0–100 | |  
| Parasitology | Float | First Parasitology mock exam score | 0–100 | |  
| Pharmacology | Float | First Pharmacology mock exam score | 0–100 | |  
| Pathology | Float | First Pathology mock exam score | 0–100 | |  
| Zootechnics | Float | First Zootechnics mock exam score | 0–100 | |  
| Microbiology & Public Health | Float | First Microbiology & Public Health score | 0–100 | |  
| Medicine | Float | First Medicine mock exam score | 0–100 | |  
| Surgery | Float | First Surgery mock exam score | 0–100 | |  
| Post-assessment 2025 | Float | First post-assessment score | 0–100 | May contain missing values |

\---

\#\# 3\. Last Attempt Scores

| Variable Name | Type | Description | Allowed Values | Notes |  
|---|---|---|---|---|  
| Pre-assessment 2025\_last | Float | Most recent pre-assessment score | 0–100 | |  
| Anatomy\_last | Float | Most recent Anatomy score | 0–100 | |  
| Physiology\_last | Float | Most recent Physiology score | 0–100 | |  
| Parasitology\_last | Float | Most recent Parasitology score | 0–100 | |  
| Pharmacology\_last | Float | Most recent Pharmacology score | 0–100 | |  
| Pathology\_last | Float | Most recent Pathology score | 0–100 | |  
| Zootechnics\_last | Float | Most recent Zootechnics score | 0–100 | |  
| Microbiology & Public Health\_last | Float | Most recent Microbiology & Public Health score | 0–100 | |  
| Medicine\_last | Float | Most recent Medicine score | 0–100 | |  
| Surgery\_last | Float | Most recent Surgery score | 0–100 | |  
| Post-assessment 2025\_last | Float | Most recent post-assessment score | 0–100 | May contain missing values |

\---

\#\# 4\. Best Attempt Scores

| Variable Name | Type | Description | Allowed Values | Notes |  
|---|---|---|---|---|  
| Pre-assessment 2025\_best | Float | Highest pre-assessment score achieved | 0–100 | |  
| Anatomy\_best | Float | Highest Anatomy score achieved | 0–100 | |  
| Physiology\_best | Float | Highest Physiology score achieved | 0–100 | |  
| Parasitology\_best | Float | Highest Parasitology score achieved | 0–100 | |  
| Pharmacology\_best | Float | Highest Pharmacology score achieved | 0–100 | |  
| Pathology\_best | Float | Highest Pathology score achieved | 0–100 | |  
| Zootechnics\_best | Float | Highest Zootechnics score achieved | 0–100 | |  
| Microbiology & Public Health\_best | Float | Highest Microbiology & Public Health score achieved | 0–100 | |  
| Medicine\_best | Float | Highest Medicine score achieved | 0–100 | |  
| Surgery\_best | Float | Highest Surgery score achieved | 0–100 | |  
| Post-assessment 2025\_best | Float | Highest post-assessment score achieved | 0–100 | May contain missing values |

\---

\#\# 5\. Engineered Features

| Variable Name | Type | Description | Allowed Values | Notes |  
|---|---|---|---|---|  
| avg\_best\_score | Float | Average of best scores across all subjects | Continuous | Reflects peak performance |  
| max\_best\_score | Float | Highest score achieved across subjects | Continuous | Indicates strongest subject |  
| avg\_first\_score | Float | Average of first attempt scores | Continuous | Baseline academic level |  
| avg\_last\_score | Float | Average of last attempt scores | Continuous | Final readiness |  
| total\_attempts | Int64 | Total number of exam attempts | ≥1 | Proxy for engagement |  
| avg\_attempts | Float | Average attempts per subject | ≥1 | Study behavior indicator |  
| avg\_improvement | Float | Average score improvement (last − first) | Can be negative | Learning progress |  
| score\_std | Float | Standard deviation of scores | ≥0 | Measures consistency |  
| num\_exams | Int64 | Number of exams taken | ≥1 | Coverage of subjects |

\---

\#\# 6\. Target Variable

| Variable Name | Type | Description | Allowed Values | Notes |  
|---|---|---|---|---|  
| Licensure Exam Result | Binary | Final licensure exam outcome | 0 \= Fail, 1 \= Pass | Target variable |

\---

\#\# 7\. Data Source

\- Source: BoardPrep internal dataset (2025 Veterinary Licensure Review Cohort)  
\- Data Type: Aggregated student-level mock exam performance data  
\- Collection Method: Extracted from BoardPrep Classroom platform 

—

\#\# 8\. Data Leakage Considerations

\- Post-assessment and last/best scores may introduce leakage if they occur too close to the licensure exam.  
\- Only features available before intervention cutoff should be used in production models.

—

\#\# 9\. Modeling Scope

\- Only features available before final licensure examination are included in model training.  
\- Temporal ordering of features is respected to prevent data leakage.  
\- Engineered features are derived solely from historical mock exam performance.

— 

\#\# Notes

\- Dataset is structured at the \*\*student level (one row per student)\*\*.  
\- Score variables are expected to range between \*\*0 and 100\*\*.  
\- Missing values in later assessments likely indicate \*\*incomplete participation\*\*, not data errors.  
\- Categorical variables (e.g., Gender) require \*\*standardization\*\* before modeling.  
\- Engineered features capture \*\*learning trajectory, engagement, and consistency\*\*, which are critical for predictive modeling.

\- Target variable (Licensure Exam Result) is collected AFTER all mock exam data.  
