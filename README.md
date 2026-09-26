# US Healthcare Analysis Case Study_1
Strategic case study analyzing 10,000 US healthcare records to optimize patient costs and hospital resource management.
# US Healthcare Cost, Demographic & Operational Analysis

## 📌 Executive Summary
This project analyzes patient admissions, clinical profiles, and financial data across 100 hospital facilities encompassing 10,000 patient records. Conducted to resolve key strategic inquiries posed by healthcare executive leadership, this analysis evaluates the interplay between patient demographics, admission streams, inpatient expenditure, and operational bed utilization.

## 🎯 Business Problem & Core Objectives
Hospital executive leadership commissioned this analysis to evaluate operational efficiency, clinical trends, and financial drivers across three distinct focus areas:
1. **Demographic Analysis of Medical Conditions:** Quantify condition prevalence across Mutually Exclusive, Collectively Exhaustive (MECE) age and gender cohorts.
2. **Patient Price Optimization:** Identify structural cost variations across admission categories, conditions, and insurance providers to propose cost-mitigation strategies.
3. **Hospital Resource Management:** Examine time-series patterns in patient flow and inpatient Length of Stay (LoS) to optimize hospital capacity and staffing allocation.

## 🗂 Dataset Overview
* **Dataset Scope:** 10,000 patient admission records.
* **Key Attributes Analyzed:**
  * **Demographic:** `Age`, `Gender`, `Blood Type`.
  * **Clinical:** `Medical Condition`, `Medication`, `Test Results`.
  * **Operational:** `Date of Admission`, `Discharge Date`, `Admission Type` (Emergency, Urgent, Elective), `Hospital`, `Doctor`, `Room Number`.
  * **Financial:** `Insurance Provider`, `Billing Amount`.

## 🧹 Data Cleaning & Preprocessing
To establish data integrity for reporting, raw data underwent standardized extract, transform, load (ETL) processing:
* **Dimensionality Reduction:** Identified and purged 11 entirely unpopulated auxiliary columns (`Column1`, `_1` through `_10`).
* **Categorical Normalization:**
  * Cleaned text fields to eliminate inconsistent spacing (e.g., mapped trailing whitespace `"M "` to `"Male"`).
  * Standardized inconsistent categorical values (e.g., converted truncated entry `"Emer "` to `"Emergency"`).
  * Harmonized case sensitivity across clinical conditions and pharmacological records.
* **Type Conversion & Feature Engineering:**
  * Converted date attributes to standardized DateTime structures and derived **Length of Stay (LoS)**:
    $$\text{Length of Stay} = \text{Discharge Date} - \text{Date of Admission}$$
  * Converted currency figures to clean numeric variables for financial aggregation.
  * Segmented patient age into three MECE operational cohorts:
    * **Young:** `<30` years
    * **Middle-Aged:** `31–60` years
    * **Seniors:** `60+` years

## ⚙️ Technical Excel & Analytical Implementations
* **Power Query (M):** Automated raw data ingestion, column filtering, string trimming, and categorical replacement logic.
* **Calculated Columns & Logic:**
  * Implemented date differential logic (`DATEDIF` / Date subtraction) to compute patient Length of Stay.
  * Applied nested logical conditions (`IFS` / `SWITCH`) to categorize age brackets into standardized demographic cohorts.
* **Pivot Modeling & Multi-Level Aggregation:** Structured cross-tabulated views isolating average billing amount, median length of stay, and patient admission counts grouped by payer, condition, and admission channel.
* **Visual Formatting & KPI Indicators:** Applied dynamic Conditional Formatting color scales and data bars across operational sheets to flag bed occupancy concentrations and outliers.

## 📊 Strategic Findings & Analytical Breakdown

### 1. Demographic Analysis of Medical Conditions
* **Hypertension Burden:** Stands as the most frequent primary diagnosis across the network (2,155 cases). Occurrence skews heavily male (1,319 male cases vs. 836 female cases) and expands progressively with age, culminating in 902 admissions among seniors (60+).
* **Asthma Age Inversion:** Unlike chronic degenerative conditions, asthma hospitalizations skew toward the younger population, peaking in the Young (<30) cohort at 680 admissions and decreasing to 339 in middle age.
* **Obesity Cohort Variation:** Documented cases of obesity-related admissions appear significantly higher in female cohorts (1,015 cases) relative to male cohorts (612 cases).
* **Cohort Summary:**
  * **Young (<30):** Dominated by Asthma (680) and Hypertension (540).
  * **Middle-Aged (30–60):** Led by Hypertension (681) and Obesity (560).
  * **Seniors (60+):** Highly concentrated in Hypertension (902), Arthritis (825), and Cancer (803).

### 2. Patient Price Optimization
* **High-Cost Clinical Categories:** Average billing per patient varies heavily based on medical diagnosis:
  * **Cancer:** $39,653 average billing.
  * **Diabetes:** $30,080 average billing.
  * **Asthma:** $22,651 average billing.
  * **Arthritis:** $20,055 average billing.
  * **Hypertension:** $17,640 average billing.
  * **Obesity:** $12,516 average billing.
* **Admission Channel Variance:** Unscheduled Emergency visits produce the highest average cost ($24,291), exceeding Elective procedures ($23,025) and Urgent admissions ($22,731).
* **Payer Distribution:** Cigna ($24,201) and Aetna ($24,125) exhibit the highest average claims burden, while Blue Cross ($22,787) and UnitedHealthcare ($22,913) maintain lower average billing figures.

### 3. Hospital Resource Management
* **Bed Occupancy & Length of Stay (LoS):**
  * **Emergency Admissions:** Average 15.62 days per patient.
  * **Urgent Admissions:** Average 15.42 days per patient.
  * **Elective Admissions:** Average 9.97 days per patient.
* **Weekly Admission Dynamics:** Patient intake remains stable throughout the week, reaching a weekday peak on Tuesdays (1,475 admissions) and a slight dip on Sundays (1,362 admissions).

---

## 💡 Strategic Recommendations & Expected Impact

| Focus Area | Identified Bottleneck | Proposed Strategic Initiative | Target Metric / KPI |
|---|---|---|---|
| **High-Cost Disease Management** | Oncology ($39.7k) and Diabetes ($30.1k) generate the highest average invoices | Expand subsidized outpatient diabetes monitoring and preventive cancer screenings | 15% reduction in preventable acute diabetic crisis hospitalizations |
| **Emergency Ward Triage** | Emergency intake carries the highest cost ($24.3k) and longest stay (15.6 days) | Establish dedicated rapid-triage routing non-critical presentations to outpatient Urgent Care | 10% reduction in low-acuity Emergency Department admissions |
| **Bed Capacity Balancing** | Midweek admission peaks (1,475) contrast with weekend lows (1,362) | Schedule short-stay Elective procedures (9.9-day LoS) exclusively on Thursdays–Saturdays | Maintain bed occupancy below an 85% operational threshold |
| **Discharge Velocity** | Long LoS in Emergency and Urgent units (15.5+ days) ties up bed capacity | Standardize multidisciplinary discharge rounds starting at day 10 of admission | 1.5-day reduction in average inpatient Length of Stay |

---

## 📁 Repository Structure
```text
├── data/
│   └── US Healthcare Case Study Practise.xlsx    # Cleaned multi-sheet analytical workbook
├── dashboards/
│   ├── Dashboard_1.png                           # Executive Overview visual dashboard
│   └── Dashboard_2.png                           # Resource Utilization & Financial breakdown
├── docs/
│   └── Overview_Questions.png                   # Original executive scope and problem statement
└── README.md                                     # Project documentation and summary
