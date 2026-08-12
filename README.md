# Fraud Detection & Payment Risk Analytics

## 📌 Project Overview

This project analyzes a large-scale financial transaction dataset to identify **fraudulent transaction patterns, abnormal transaction behavior, high-risk customers, merchant-level anomalies, geographic risk, and potential fraud indicators**.

The project follows an end-to-end fraud analytics workflow:

**Raw Transaction Data → Data Preparation → SQL Investigation → Fraud Feature Engineering → Statistical & Anomaly Analysis → Risk Scoring → Power BI Monitoring → Investigation Prioritization → Risk Recommendations**

The objective is not simply to identify transactions that are already labeled as fraudulent, but to understand **why transactions may represent elevated risk**, identify recurring behavioral patterns, segment transactions and customers by risk, and convert analytical findings into monitoring metrics that can support fraud investigation and prevention.

The repository combines **SQL, Python/statistical analysis, risk scoring, data preparation, and Power BI** to demonstrate a practical financial fraud analytics workflow.

---

## 🎯 Business Problem

Financial transaction systems generate large volumes of transactions across customers, merchants, payment methods, devices, countries, and time periods.

Fraud teams need to answer questions such as:

* What percentage of transactions are fraudulent?
* Which merchant categories have the highest fraud rates?
* Which countries show elevated fraud activity?
* Are certain payment methods associated with higher fraud risk?
* Are fraudulent transactions concentrated during specific hours?
* Are newly created accounts more exposed to fraud?
* Which customers generate the highest number or value of fraudulent transactions?
* Are customers transacting outside their home country?
* Are there unusually high transaction frequencies within short periods?
* Which transactions contain multiple risk indicators?
* Which customers should investigators prioritize?
* What risk indicators should be continuously monitored?

This project addresses these questions by transforming transaction-level data into **fraud indicators, risk segments, investigation metrics, and actionable recommendations**.

---

# 📊 Dataset

The analytical dataset contains **15,000 financial transactions** with customer, transaction, merchant, geographic, payment, behavioral, and fraud-related attributes.

The main transaction structure contains fields including:

* `transaction_id`
* `customer_id`
* `transaction_date`
* `amount`
* `merchant_id`
* `merchant_category`
* `payment_method`
* `device_type`
* `device_id`
* `ip_address`
* `transaction_country`
* `chargeback`
* `is_fraud`

Customer-level attributes include:

* `customer_name`
* `age`
* `account_age_days`
* `home_country`
* `email_domain`
* `is_vip`

The SQL database design establishes a customer table and a transaction table connected through `customer_id`.

---

# 📈 Key Dataset Metrics

| Metric                   |        Value |
| ------------------------ | -----------: |
| Total Transactions       |       15,000 |
| Fraud Cases              |        3,585 |
| Fraud Rate               |       23.90% |
| Total Transaction Amount | 1,505,790.52 |
| Fraud Transaction Amount |   366,267.93 |

These metrics are also available in the project's KPI output.

---

# 🧩 Technology Stack

### SQL

Used for:

* Transaction-level investigation
* Fraud-rate calculation
* Aggregation and segmentation
* Customer risk analysis
* Merchant analysis
* Geographic analysis
* Time-based fraud analysis
* Behavioral anomaly identification
* Cross-border transaction analysis
* Risk ranking
* Analytical views

### Python

Used as part of the analytical workflow for:

* Exploratory Data Analysis
* Data profiling
* Statistical analysis
* Feature engineering
* Fraud-pattern exploration
* Anomaly detection
* Class-imbalance analysis
* Risk segmentation
* Analytical validation

### Power BI

Used for:

* Fraud monitoring
* KPI reporting
* Risk segmentation
* Geographic analysis
* Transaction anomaly monitoring
* Fraud trend analysis
* Investigation prioritization
* Executive-level risk reporting

### Data & Analytics Concepts

* Exploratory Data Analysis
* Fraud Analytics
* Risk Analytics
* Feature Engineering
* Anomaly Detection
* Statistical Analysis
* Customer Segmentation
* Risk Scoring
* Behavioral Analysis
* KPI Development
* Data Visualization
* Investigation Prioritization

---

# 🔍 Analytical Workflow

## 1. Data Understanding & Preparation

The first stage involved understanding the structure of customer and transaction data.

The transaction dataset combines:

**Customer Information**

* Customer identity
* Account age
* Home country
* VIP status
* Demographic attributes

**Transaction Information**

* Transaction amount
* Transaction timestamp
* Merchant
* Merchant category
* Payment method
* Device type
* Device identifier

**Risk & Fraud Information**

* Fraud indicator
* Chargeback indicator
* Transaction country
* Cross-border behavior
* High-value transaction behavior
* Late-night activity
* New-account activity

The data was structured so that transaction-level behavior could be analyzed alongside customer-level characteristics.

---

# 🧮 2. SQL Fraud Investigation

SQL was used as the primary investigation layer to analyze transaction behavior and identify potential fraud patterns.

The SQL analysis calculates overall fraud metrics and breaks fraud activity down across multiple dimensions.

## Fraud Rate Analysis

The project calculates:

* Total transactions
* Total fraud transactions
* Overall fraud rate

This establishes the baseline fraud level against which individual segments can be compared.

---

## Chargeback Analysis

Chargebacks were analyzed as an additional risk indicator by calculating:

* Total transactions
* Total chargebacks
* Chargeback rate

This provides another perspective on transaction risk beyond the `is_fraud` label.

---

## Merchant Category Analysis

Fraud activity was segmented by merchant category to identify categories with elevated fraud rates.

Analysis includes:

* Transaction volume
* Fraud transaction count
* Fraud rate
* Ranking of merchant categories by fraud rate

This helps identify merchant segments that may require additional monitoring.

---

## Geographic Fraud Analysis

Transactions were analyzed by `transaction_country` to identify geographic concentrations of fraud.

The analysis compares:

* Transaction volume
* Fraud volume
* Fraud rate

This can help identify geographic segments that require additional investigation.

---

## Payment Method Analysis

Fraud was also analyzed across different payment methods.

The analysis compares fraud rates between methods such as:

* Credit card
* Debit card
* Bank transfer
* PIX
* Other available payment methods

This allows payment channels with elevated fraud exposure to be identified.

---

# 💰 3. Transaction Amount Analysis

Transaction amounts were analyzed separately for fraudulent and non-fraudulent transactions.

The SQL workflow calculates:

* Average transaction amount
* Maximum transaction amount
* Minimum transaction amount
* Fraud vs. non-fraud transaction value

This helps identify whether unusually large transactions are associated with increased fraud exposure.

The project also defines a **high-value transaction indicator** for transactions above the configured threshold of `3000`.

---

# 👤 4. Customer Fraud Analysis

Customer-level analysis was performed to identify customers with significant fraud activity.

The analysis combines:

* Total transactions
* Fraud transactions
* Total transaction amount
* Fraud transaction amount

Customers are then ranked based on fraud activity and fraud value.

This creates an investigation-oriented view where analysts can focus on customers generating a disproportionately high amount of suspicious activity.

---

# ⏰ 5. Time-Based Fraud Analysis

Transaction timestamps were analyzed to identify temporal patterns.

The project investigates fraud activity by transaction hour to determine whether specific time periods have elevated fraud rates.

A dedicated late-night indicator is also created for transactions occurring between:

**00:00 – 05:00**

This provides a behavioral signal that can be combined with other risk indicators.

---

# 🆕 6. New Account Risk Analysis

Customer account age was incorporated into fraud analysis.

Accounts are segmented into:

* **New Account:** `< 30 days`
* **Mid Account:** `30–180 days`
* **Mature Account:** `> 180 days`

Fraud rates are then compared across these account-age segments.

A separate `new_account_flag` is also created for customers with account age below 30 days.

This allows new-account behavior to be evaluated as a potential fraud indicator.

---

# ⚡ 7. Transaction Frequency & Velocity Analysis

Transaction velocity was investigated by identifying customers with multiple transactions occurring within a short time period.

The SQL workflow groups transactions by:

* Customer
* Transaction hour

Customers with **5 or more transactions within the same hour** are flagged for further investigation.

This provides a transaction-velocity signal that can identify potentially abnormal bursts of activity.

---

# 🌍 8. Cross-Border Transaction Analysis

Customer home country was compared with transaction country.

A transaction is treated as cross-border when:

`transaction_country <> home_country`

This creates a behavioral risk indicator that can be used to identify customers performing transactions outside their expected geographic pattern.

The project also counts cross-border transactions at the customer level to support risk ranking.

---

# 🧠 9. Fraud Feature Engineering

Multiple transaction-level risk indicators were engineered from the available customer and transaction attributes.

### High-Value Flag

Identifies transactions above the configured high-value threshold.

### Cross-Border Flag

Identifies transactions occurring outside the customer's home country.

### Late-Night Flag

Identifies transactions occurring between 00:00 and 05:00.

### New Account Flag

Identifies transactions associated with customers whose accounts are less than 30 days old.

### High-Risk Merchant Flag

Identifies transactions associated with merchant categories or merchants considered higher risk within the analytical framework.

These engineered features transform raw transaction attributes into interpretable **fraud signals**.

---

# 🚨 10. Risk Scoring Framework

The project combines multiple behavioral indicators into a customer-level risk score.

The risk framework considers:

* High-value transactions
* Cross-border transactions
* Late-night transactions
* New-account activity
* Confirmed fraud activity

The customer risk score applies weighted contributions to these indicators.

The implemented scoring logic assigns greater weight to cross-border activity and confirmed fraud transactions, while high-value, late-night, and new-account activity contribute additional risk points.

This converts multiple individual indicators into a consolidated customer risk profile.

---

# 📊 Risk Distribution

The processed dataset contains four risk segments:

| Risk Level | Transactions | Transaction Amount |
| ---------- | -----------: | -----------------: |
| Critical   |           21 |           3,197.72 |
| High       |        3,153 |         316,578.66 |
| Medium     |        9,564 |         956,449.36 |
| Low        |        2,262 |         229,564.78 |

The risk distribution is available in the project's processed analytical output.

This segmentation supports an investigation-prioritization framework where higher-risk activity can be reviewed before lower-risk transactions.

---

# 🐍 11. Python & Statistical Fraud Analysis

Python was used as an analytical layer to complement the SQL investigation.

The Python/statistical workflow focuses on understanding the distribution and behavior of fraudulent transactions rather than relying only on binary fraud labels.

Key analytical areas include:

### Exploratory Data Analysis

* Distribution of transaction amounts
* Fraud vs. non-fraud comparison
* Transaction frequency
* Customer activity
* Merchant activity
* Geographic patterns
* Temporal patterns
* Risk-segment distributions

### Feature Engineering

Derived features were used to represent behavioral risk, including:

* High-value transaction behavior
* Cross-border behavior
* Late-night behavior
* New-account behavior
* Merchant risk
* Composite risk indicators

### Anomaly Detection

Transaction behavior was examined for unusual patterns such as:

* High transaction values
* Unusual transaction frequency
* Short-interval transaction bursts
* Cross-border activity
* Late-night transactions
* Multiple simultaneous risk indicators

### Class Imbalance Analysis

Fraud detection is inherently a classification problem where fraudulent transactions may not represent the majority of transaction activity.

The analysis therefore considers:

* Fraud vs. non-fraud distribution
* Fraud-rate interpretation
* Segment-level fraud rates
* Risk-segment concentration

This prevents overall transaction volume from hiding meaningful fraud patterns within smaller segments.

---

# 📊 12. Power BI Fraud Monitoring Dashboard

The processed transaction data was prepared for Power BI to create a fraud-monitoring environment.

The dashboard is designed around four major analytical perspectives.

## Executive Fraud Monitoring

Provides a high-level view of:

* Total transactions
* Fraud cases
* Fraud rate
* Fraud amount
* Transaction volume
* Risk distribution

This view is intended for management and fraud-risk stakeholders.

---

## Investigation Analysis

Supports deeper investigation of:

* Suspicious transactions
* High-risk customers
* Fraud amount
* Risk levels
* Transaction characteristics
* Fraud indicators
* Merchant activity

The objective is to move from a high-level fraud KPI into transaction and customer-level investigation.

---

## Geographic Monitoring

Analyzes:

* Fraud by country
* Transaction volume by country
* Geographic fraud rate
* Cross-border activity

This allows geographic risk concentrations to be identified.

---

## Temporal Monitoring

Analyzes:

* Fraud trends over time
* Transaction volume over time
* Fraud by transaction hour
* Late-night activity
* Transaction anomalies

This helps identify changes in fraud behavior across time.

---

# 📌 Investigation KPIs

The analytical workflow supports monitoring of:

* Total Transactions
* Fraud Transactions
* Fraud Rate
* Fraud Amount
* Average Transaction Amount
* Chargeback Rate
* High-Risk Transactions
* High-Value Transactions
* Cross-Border Transactions
* Late-Night Transactions
* New-Account Transactions
* Risk-Level Distribution
* Customer Fraud Concentration
* Merchant Fraud Rate
* Geographic Fraud Rate

These KPIs convert detailed transaction-level analysis into metrics that can be monitored by fraud and risk teams.

---

# 🔎 Key Fraud Signals

The project identifies several behavioral signals that can be used as inputs to fraud investigation.

### 1. High Transaction Value

Transactions above the configured threshold may represent increased financial exposure.

### 2. Cross-Border Activity

Transactions occurring outside a customer's home country may indicate unusual geographic behavior.

### 3. Late-Night Activity

Transactions between midnight and 5 AM are treated as a behavioral risk indicator.

### 4. New Account Activity

Transactions involving accounts less than 30 days old receive additional risk consideration.

### 5. Transaction Velocity

Multiple transactions by the same customer within a short period can indicate abnormal transaction behavior.

### 6. Merchant Risk

Certain merchant categories or merchants can exhibit higher fraud exposure and therefore require additional monitoring.

### 7. Confirmed Fraud History

Previous fraudulent activity significantly increases the customer's overall risk score.

---

# 🧮 SQL Techniques Demonstrated

The SQL portion demonstrates practical analytical SQL including:

* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`
* `ROUND()`
* `CASE WHEN`
* `GROUP BY`
* `HAVING`
* `ORDER BY`
* `LIMIT`
* `JOIN`
* Date/time extraction
* `DATE_TRUNC()`
* Conditional aggregation
* Customer-level aggregation
* Risk ranking
* Analytical views

The advanced SQL workflow contains 12 dedicated fraud-analysis investigations covering fraud rate, chargebacks, merchant/category analysis, geography, payment method, transaction values, customer fraud, time-of-day behavior, account age, velocity, cross-border activity, and customer risk ranking.

---

# 🗂️ Repository Structure

```text
Fraud-Detection-Payment-Risk-Analytics/
│
├── 01_create_tables.sql
├── 02_insert_data.sql
├── 03_advanced_queries.sql
├── 04_views.sql
│
├── Data/
│
├── customers raw data.csv
├── transactions raw data.csv
├── final_transactions_for_bi.csv
├── transactions_scored.csv
│
├── fraud_by_category.csv
├── fraud_by_country.csv
├── risk_distribution.csv
├── kpis.csv
│
├── fraud_dashboard.pbix
│
├── image_dashboard_executivo.png
├── image_dashboard_investigativo.png
├── image_dashboard_temporal.png
│
├── business_context.md
├── fraud_rules.md
│
└── README.md
```

The repository includes SQL table creation, data insertion, advanced fraud-analysis queries, analytical views, raw and processed transaction data, KPI outputs, risk-distribution outputs, and the Power BI dashboard assets.

---

# 🔄 End-to-End Analytical Architecture

```text
                    RAW TRANSACTION DATA
                             │
                             ▼
                  DATA PREPARATION & JOINING
                             │
                             ▼
                    CUSTOMER + TRANSACTION
                           MODEL
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
          SQL ANALYSIS              PYTHON / STATISTICS
              │                             │
              │                    ┌────────┴────────┐
              │                    │                 │
              │                    ▼                 ▼
              │              EDA / FEATURES    ANOMALY ANALYSIS
              │                    │                 │
              └──────────────┬─────┴─────────────────┘
                             ▼
                    FRAUD SIGNAL GENERATION
                             │
                             ▼
                      RISK SCORING
                             │
                             ▼
                    RISK SEGMENTATION
                             │
                             ▼
                    POWER BI MONITORING
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
          FRAUD KPIs     RISK ANALYSIS   INVESTIGATION
                                          PRIORITIZATION
                             │
                             ▼
                   ACTIONABLE RISK INSIGHTS
```

---

# 💡 Business Insights & Recommendations

The analysis supports several practical fraud-management recommendations.

### Prioritize High-Risk Customers

Customers with multiple risk indicators and previous fraud activity should receive higher investigation priority.

### Monitor Transaction Velocity

High-frequency transaction bursts should be monitored as potential abnormal behavior.

### Strengthen Cross-Border Monitoring

Customers performing transactions outside their normal geographic profile should receive additional risk consideration.

### Monitor New Accounts

Newly created accounts should receive enhanced monitoring, particularly when combined with other risk signals.

### Monitor High-Value Transactions

Large transactions should be evaluated against customer history and other behavioral indicators rather than assessed in isolation.

### Segment Merchant Risk

Merchant categories with elevated fraud rates can be targeted for enhanced monitoring and fraud controls.

### Monitor Time-Based Patterns

Late-night transaction activity can be incorporated into behavioral risk monitoring.

### Use Risk-Based Investigation

Instead of investigating every transaction equally, investigation resources can be prioritized according to:

**Risk Level → Fraud Indicators → Customer History → Transaction Value → Behavioral Anomalies**

---

# 🎯 Analytical Outcome

The project transforms raw financial transaction records into a structured fraud-risk analytics framework.

The final workflow enables stakeholders to move from:

**Raw Data**

→ Transaction Analysis

→ Fraud Pattern Identification

→ Behavioral Feature Engineering

→ Anomaly Detection

→ Risk Scoring

→ Customer & Transaction Segmentation

→ Fraud Monitoring

→ Investigation Prioritization

→ Actionable Risk Recommendations

This demonstrates how SQL, Python/statistical analysis, and Power BI can be combined to solve a practical **financial fraud detection and payment risk analytics** problem.

---

# 🧠 Skills Demonstrated

### Data Analysis

* Exploratory Data Analysis
* Fraud Analytics
* Risk Analytics
* Behavioral Analytics
* Anomaly Detection
* Statistical Analysis
* Class Imbalance Analysis
* Feature Engineering
* Risk Segmentation

### SQL

* Advanced Aggregations
* Joins
* Conditional Logic
* Date/Time Analysis
* Customer-Level Analysis
* Merchant Analysis
* Geographic Analysis
* Fraud Rate Analysis
* Risk Scoring
* Analytical Views

### Python

* Data Analysis
* Statistical Analysis
* Feature Engineering
* Anomaly Detection
* Fraud Pattern Analysis
* Risk Segmentation

### Power BI

* Fraud Monitoring Dashboard
* KPI Development
* Risk Segmentation
* Geographic Analysis
* Temporal Analysis
* Investigation Reporting
* Data Visualization

### Business & Risk

* Fraud Detection
* Payment Risk
* Transaction Monitoring
* Investigation Prioritization
* Risk Indicators
* Actionable Recommendations
* Fraud Prevention Analytics

---

# 📁 Project Files

| File                            | Purpose                                                            |
| ------------------------------- | ------------------------------------------------------------------ |
| `01_create_tables.sql`          | Creates customer and transaction database tables                   |
| `02_insert_data.sql`            | Loads transaction/customer data                                    |
| `03_advanced_queries.sql`       | Contains fraud investigation and analytical SQL queries            |
| `04_views.sql`                  | Creates fraud-summary and customer-risk analytical views           |
| `transactions raw data.csv`     | Raw transaction dataset                                            |
| `customers raw data.csv`        | Raw customer dataset                                               |
| `final_transactions_for_bi.csv` | Processed dataset prepared for BI analysis                         |
| `transactions_scored.csv`       | Transactions containing engineered risk indicators and risk scores |
| `fraud_by_category.csv`         | Fraud analysis by merchant category                                |
| `fraud_by_country.csv`          | Geographic fraud analysis                                          |
| `risk_distribution.csv`         | Risk-level distribution                                            |
| `kpis.csv`                      | Key fraud monitoring metrics                                       |
| `fraud_dashboard.pbix`          | Power BI fraud monitoring dashboard                                |

---

# 🚀 Conclusion

This project demonstrates an end-to-end approach to **financial fraud detection and payment risk analytics**, combining transactional investigation, customer behavior analysis, statistical exploration, anomaly detection, feature engineering, risk scoring, SQL analytics, and Power BI visualization.

The key objective was to convert large volumes of raw transaction data into a structured decision-support system capable of identifying:

* Fraud patterns
* Abnormal behavior
* High-risk customers
* High-risk transactions
* Geographic anomalies
* Merchant-level risk
* Transaction velocity
* Behavioral risk indicators
* Investigation priorities

The result is a practical analytical framework that can support **fraud monitoring, transaction investigation, risk segmentation, and data-driven fraud prevention**.

---

## 🔗 Project Repository

[Fraud Detection & Payment Risk Analytics](https://github.com/Aksmalik/Fraud-Detection-Payment-Risk-Analytics)

