# 🏦 Bank Loan Portfolio Analysis

### SQL | Power BI | Power Query | Data Analysis | MS Excel | Financial Analytics | KPI Reporting 

> An end-to-end **Bank Loan Portfolio Analysis** project using SQL and Power BI to evaluate lending performance, portfolio quality, borrower characteristics, repayment behavior, and regional trends.

---

## 📌 Project Overview

This project analyzes a bank loan portfolio containing **38,576 loan records** to understand lending performance and portfolio health.

The analysis combines **SQL-based data analysis** with an interactive **Power BI dashboard** to transform raw loan data into actionable financial insights.

The project focuses on:

* Loan application performance
* Funded and received amounts
* Good vs. bad loan performance
* Loan status analysis
* Interest rate and DTI trends
* Monthly lending trends
* Geographic performance
* Loan term distribution
* Employment characteristics
* Loan purpose analysis
* Home ownership patterns

The project follows a business-oriented approach rather than simply presenting charts: **identify the business problem → define KPIs → analyze the portfolio → visualize findings → support data-driven decisions.**

---

# ⭐ Business Case Study — STAR Framework

## 🟦 S — Situation

Banks manage large volumes of loan applications and repayment records. Monitoring this data manually makes it difficult to quickly understand:

* How much money has been funded
* How much has been recovered
* Whether the loan portfolio is performing well
* Which loans are considered good or bad
* How lending activity changes over time
* Which borrower segments contribute most to lending activity
* How loan performance differs across states and loan purposes

The project documentation identifies the need for a comprehensive Bank Loan Report to monitor lending activities, portfolio health, and trends over time.

### Dataset Scale

| Metric                 |        Value |
| ---------------------- | -----------: |
| Loan Records Analyzed  |   **38,576** |
| Total Funded Amount    | **$435.76M** |
| Total Amount Received  | **$473.07M** |
| Average Interest Rate  |   **12.05%** |
| Average DTI            |   **13.33%** |
| Good Loan Applications |   **33,243** |
| Good Loan Percentage   |   **86.18%** |
| Bad Loan Applications  |    **5,333** |
| Bad Loan Percentage    |   **13.82%** |

> **Note:** Financial figures are calculated directly from the supplied loan dataset. Percentages follow the project definition of Good Loans = `Fully Paid + Current` and Bad Loans = `Charged Off`.

---

# 🟨 T — Task

The objective was to build a **decision-oriented loan analytics solution** that could help stakeholders monitor portfolio performance through standardized KPIs and interactive visualizations.

### Key Business Questions

1. How many loan applications were received?
2. How much was funded?
3. How much was received from borrowers?
4. What is the average interest rate?
5. What is the average borrower DTI?
6. What percentage of loans are performing well?
7. What percentage of loans are charged off?
8. How does lending activity change month-over-month?
9. Which states generate the highest lending activity?
10. How are loans distributed across different terms?
11. Which employment groups have the highest loan activity?
12. What are the major reasons borrowers take loans?
13. How does home ownership relate to loan activity?
14. How do loan metrics differ by loan status?

The requested KPI framework includes Total Applications, Total Funded Amount, Total Amount Received, Average Interest Rate, and Average DTI, including MTD and month-over-month analysis.

---

# 🟩 A — Action

## 1. Data Preparation

Analyzed the raw loan dataset containing **38,576 records and 24 fields**.

Key fields included:

* Loan ID
* State
* Application Type
* Employment Length
* Employment Title
* Grade / Sub-Grade
* Home Ownership
* Issue Date
* Loan Status
* Purpose
* Term
* Verification Status
* Annual Income
* DTI
* Installment
* Interest Rate
* Loan Amount
* Total Payment

## These fields provide information about borrower characteristics, loan risk classification, loan terms, repayment behavior, and portfolio performance.

## 2. SQL Analysis

Built SQL queries to calculate portfolio-level KPIs and segment the loan portfolio.

### Core KPIs

```sql
-- Total Loan Applications
SELECT COUNT(id) AS Total_Applications
FROM bank_loan_data;

-- Total Funded Amount
SELECT SUM(loan_amount) AS Total_Funded_Amount
FROM bank_loan_data;

-- Total Amount Received
SELECT SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data;

-- Average Interest Rate
SELECT AVG(int_rate) * 100 AS Avg_Int_Rate
FROM bank_loan_data;

-- Average DTI
SELECT AVG(dti) * 100 AS Avg_DTI
FROM bank_loan_data;
```

## The KPI definitions and corresponding SQL approach are based on the project query requirements.

## 3. Good vs. Bad Loan Analysis

Created portfolio-quality metrics using loan status.

### Good Loans

Defined as:

* `Fully Paid`
* `Current`

### Bad Loans

Defined as:

* `Charged Off`

### Portfolio Result

| Portfolio Category | Applications |      Share |
| ------------------ | -----------: | ---------: |
| 🟢 Good Loans      |   **33,243** | **86.18%** |
| 🔴 Bad Loans       |    **5,333** | **13.82%** |
| **Total**          |   **38,576** |   **100%** |

The project's business definition explicitly classifies Fully Paid and Current loans as Good Loans and Charged Off loans as Bad Loans.

---

## 4. Loan Status Analysis

Analyzed portfolio performance across individual loan statuses.

| Loan Status | Applications |
| ----------- | -----------: |
| Fully Paid  |   **32,145** |
| Current     |    **1,098** |
| Charged Off |    **5,333** |
| **Total**   |   **38,576** |

This analysis allows stakeholders to distinguish between completed loans, currently active loans, and charged-off loans.

---

## 5. Monthly Performance Analysis

Created month-level analysis using the loan issue date to monitor:

* Loan applications
* Funded amount
* Amount received

```sql
SELECT
    MONTH(issue_date) AS Month_Number,
    DATENAME(MONTH, issue_date) AS Month_Name,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY
    MONTH(issue_date),
    DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date);
```

This follows the project's requirement to use monthly trends to identify changes in lending activity over time.

---

# 📊 Dashboard Design

## Dashboard 1 — Executive Summary

Designed an executive-level dashboard containing:

### KPI Cards

* Total Loan Applications
* Total Funded Amount
* Total Amount Received
* Average Interest Rate
* Average DTI
* Good Loan %
* Bad Loan %

### Loan Performance

* Good Loan Applications
* Good Loan Funded Amount
* Good Loan Amount Received
* Bad Loan Applications
* Bad Loan Funded Amount
* Bad Loan Amount Received

The report requirements specifically call for separate Good Loan and Bad Loan KPIs.

---

# 📈 Dashboard 2 — Portfolio Overview

Built an interactive overview dashboard covering multiple dimensions of the portfolio.

### 📅 Monthly Trend

**Line Chart**

Tracks:

* Loan Applications
* Funded Amount
* Amount Received

### 🗺️ Regional Analysis

**Filled Map**

Analyzes:

* Loan Applications by State
* Funded Amount by State
* Amount Received by State

### 💳 Loan Term Analysis

**Donut Chart**

Compares loan distribution across:

* 36-month loans
* 60-month loans

### 👔 Employment Analysis

**Bar Chart**

Analyzes lending activity across employment-length categories.

### 🎯 Loan Purpose

**Bar Chart**

Analyzes lending activity across purposes such as:

* Debt Consolidation
* Credit Card
* Other loan purposes

### 🏠 Home Ownership

**Treemap**

Segments lending activity by:

* Rent
* Mortgage
* Own

These visual dimensions are aligned with the project's specified dashboard requirements.

---

# 🔎 Dashboard 3 — Loan Details

Created a detailed view to allow users to explore the underlying portfolio at a more granular level.

### Key Dimensions

* Loan Status
* Grade
* Sub-Grade
* Purpose
* State
* Term
* Employment Length
* Home Ownership
* Verification Status

### Key Metrics

* Loan Applications
* Funded Amount
* Amount Received
* Interest Rate
* DTI

The Details Dashboard is intended to provide a consolidated view of loan and borrower information for deeper portfolio analysis.

---

# 💡 Key Findings

## 1. Strong Overall Portfolio Performance

**86.18%** of the analyzed applications fall into the project's Good Loan category, while **13.82%** are classified as Bad Loans.

This provides a high-level view of portfolio quality based on the defined loan-status methodology.

---

## 2. Large Lending Portfolio

The analysis covered:

> **38,576 loan applications**

representing approximately:

> **$435.76M in funded loans**

This provides a substantial dataset for evaluating lending patterns across borrowers, geography, loan terms, and purposes.

---

## 3. Repayment Activity Exceeded Funded Principal

The dataset records approximately:

> **$473.07M Total Amount Received**

against:

> **$435.76M Total Funded Amount**

The difference is approximately:

> **$37.31M**

This should be interpreted in the context of the dataset's `total_payment` field and should not automatically be treated as pure profit, since interest, timing, fees, and other financial factors are not separately isolated in this analysis.

---

## 4. Risk Segmentation

The analysis incorporates:

* Grade
* Sub-Grade
* DTI
* Interest Rate
* Loan Status
* Annual Income
* Employment Length
* Home Ownership

These variables provide multiple dimensions for understanding borrower risk and loan performance.

The domain documentation identifies risk assessment, portfolio management, fraud detection, profitability analysis, and customer insights as important applications of bank loan data analysis.

---

# 📌 Business Impact

Rather than claiming unsupported financial savings, the measurable impact of this project is represented by **analytical coverage and decision-support scale**.

### 📊 Impact at a Glance

| Impact Area                       |       Result |
| --------------------------------- | -----------: |
| Loan Records Analyzed             |   **38,576** |
| Dataset Fields                    |       **24** |
| Funded Portfolio Covered          | **$435.76M** |
| Amount Received Analyzed          | **$473.07M** |
| Good Loan Applications Identified |   **33,243** |
| Bad Loan Applications Identified  |    **5,333** |
| Good Loan Share Calculated        |   **86.18%** |
| Bad Loan Share Calculated         |   **13.82%** |
| Average Interest Rate             |   **12.05%** |
| Average DTI                       |   **13.33%** |
| Analytical Dimensions             |       **8+** |
| Dashboard Views                   |        **3** |

### Decision-Support Impact

The solution converts raw loan-level data into a structured reporting framework that enables stakeholders to:

* Monitor portfolio health
* Track lending activity
* Compare good vs. bad loans
* Identify regional lending patterns
* Analyze borrower segments
* Monitor repayment-related metrics
* Compare loan terms and purposes
* Drill down into individual portfolio dimensions

---

# 🛠️ Tech Stack

| Technology      | Usage                                           |
| --------------- | ----------------------------------------------- |
| **SQL**         | Data extraction, aggregation & KPI calculations |
| **Power BI**    | Interactive dashboards & data visualization     |
| **DAX**         | Measures and calculated metrics                 |
| **Power Query** | Data transformation & preparation               |
| **Excel / CSV** | Source data and validation                      |
| **GitHub**      | Project documentation & version control         |

---

# 🧠 SQL Concepts Used

* `COUNT()`
* `SUM()`
* `AVG()`
* `CASE WHEN`
* `GROUP BY`
* `ORDER BY`
* Date functions
* Conditional aggregation
* Monthly aggregation
* KPI calculations
* Segmentation
* Portfolio-level analysis

---

# 📐 Analytical Framework

```text
                    RAW LOAN DATA
                          │
                          ▼
                 DATA PREPARATION
                          │
                          ▼
                    SQL ANALYSIS
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
       KPIs         Loan Quality      Segmentation
          │               │               │
          ▼               ▼               ▼
    Applications     Good vs Bad      State
    Funded Amount    Loan Status      Purpose
    Amount Received                  Term
    Interest Rate                    Employment
    DTI                              Home Ownership
          │               │               │
          └───────────────┼───────────────┘
                          ▼
                    POWER BI MODEL
                          │
                          ▼
               ┌──────────┼──────────┐
               ▼          ▼          ▼
             SUMMARY    OVERVIEW   DETAILS
               │          │          │
               └──────────┼──────────┘
                          ▼
                 BUSINESS INSIGHTS
```

---

# 📂 Repository Structure

```text
Bank-Loan-Analysis/
│
├── README.md
│
├── data/
│   └── financial_loan.csv
│
├── sql/
│   └── bank_loan_analysis.sql
│
├── powerbi/
│   └── Bank_Loan_Report.pbix
│
├── dashboard/
│   ├── summary_dashboard.png
│   ├── overview_dashboard.png
│   └── details_dashboard.png
│
└── documentation/
    └── project_documentation.md
```

---

# 🚀 Project Workflow

```text
Raw Data
   ↓
Data Cleaning
   ↓
Data Validation
   ↓
SQL KPI Development
   ↓
Loan Quality Analysis
   ↓
Segmentation Analysis
   ↓
Power BI Data Model
   ↓
Dashboard Development
   ↓
Business Insights
```

---

# 🎯 Skills Demonstrated

### Data Analytics

* Exploratory Data Analysis
* KPI Development
* Financial Analytics
* Portfolio Analysis
* Segmentation
* Trend Analysis
* Risk Analysis

### SQL

* Aggregations
* Conditional Logic
* Date Analysis
* Grouping
* KPI Queries
* Portfolio Segmentation

### Business Intelligence

* Power BI
* DAX
* Power Query
* Interactive Filters
* KPI Cards
* Drill-down Analysis
* Dashboard Design

### Business Skills

* Problem Structuring
* Requirement Understanding
* Business KPI Definition
* Data Storytelling
* Financial Domain Understanding
* Decision-Support Reporting

---

# 📌 Resume-Ready Project Summary

> **Bank Loan Portfolio Analysis | SQL, Power BI, DAX, Power Query**
>
> Analyzed **38,576 loan records** covering **$435.76M in funded loans**, developing SQL-based KPIs and 3 Power BI dashboards to evaluate portfolio performance, good vs. bad loan distribution, repayment metrics, borrower segmentation, regional trends, loan purposes, and term patterns; identified **86.18% Good Loans vs. 13.82% Bad Loans** and tracked **$473.07M in total recorded payments**.

---

# 📎 Dataset & Methodology

The analysis follows the supplied Bank Loan Report requirements and domain documentation.

The source framework defines:

* Good Loans as **Fully Paid + Current**
* Bad Loans as **Charged Off**
* KPIs including Applications, Funded Amount, Amount Received, Interest Rate, and DTI
* Analysis across state, term, employment length, purpose, and home ownership.

---

# 👩‍💻 Author

### Deblina Mandal

**Computer Science Graduate | Data Analyst**

📍 India

🔗 [LinkedIn](https://www.linkedin.com/in/deblina-mandal-615507273/)

🔗 [GitHub](https://github.com/deblinamandal2002)

---

## ⭐ If you found this project useful

Feel free to ⭐ star the repository and explore the analysis.

---

### Project Focus

**Turning loan-level data into business-ready financial insights.**
