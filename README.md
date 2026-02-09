# 📊 Online Retail Cancellation & Return Analysis

## 📌 Project Overview

This project analyzes customer order cancellations using the **Online Retail II** dataset. The data tracks all transactions for a UK-based, non-store online retailer between **December 1, 2009, and December 9, 2011**.

The primary objective is to identify **high-risk customers and products driving revenue loss**. Using a combination of **risk–value segmentation**, **tenure analysis**, and **product-level diagnostics**, this analysis provides a framework for root-cause investigation and data-driven retention decisions.

* **Dataset Source:** [Online Retail II (Kaggle)](https://www.kaggle.com/datasets/lakshmi25npathi/online-retail-dataset/data)  
The final output is an **interactive Power BI dashboard** designed for business stakeholders.

* **Run Data Cleaning Notebook:**   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NabilJabre/Online-Retail-Cancellation-Return-Analysis/blob/main/Data%20Quality%26Cleaning.ipynb)

* **Click here to download the Power BI Report:** [Download Report](https://drive.google.com/uc?export=download&id=1wnRleY1lAzWQnEwqDm55p9B66r9i_S0C)
---

## 🎯 Business Problem
Order cancellations are a major source of **revenue leakage** in online retail.  
The goal of this project is to:
- Quantify the **financial impact** of cancellations
- Identify **high-value, high-risk customers**
- Detect **products with disproportionately high cancellation rates**
- Support targeted **re-engagement and retention strategies**

---

## 📁 Dataset Details

The analysis is based on the **Online Retail II** dataset, which captures the transactional history of a UK-based retailer.

### 📊 Quick Stats
* **Domain:** Online Retail Transactions
* **Size:** 1,000,000+ rows
* **Granularity:** Transactional (line-item level)
* **Timeframe:** 2009 – 2011

### 📑 Attribute Information
| Column | Data Type | Description |
| :--- | :--- | :--- |
| **InvoiceNo** | Nominal | 6-digit unique ID. Numbers starting with **'C'** indicate a cancellation. |
| **StockCode** | Nominal | 5-digit unique product/item ID (SKU). |
| **Description** | Nominal | Product name. |
| **Quantity** | Numeric | The number of units per transaction. |
| **InvoiceDate** | DateTime | The day and time the transaction was generated. |
| **UnitPrice** | Numeric | Product price per unit. |
| **CustomerID** | Nominal | 5-digit unique ID assigned to each customer. |
| **Country** | Nominal | The country where the customer resides. |

> **Note on Feature Engineering:** For this project, a **Cancellation Flag** was derived from `InvoiceNo`, and **Revenue** was calculated as `Quantity * UnitPrice`. 

---

## 🛠️ Tools & Technologies

* **Python (Pandas):** Data cleaning and complex feature engineering.
* **SQL (DuckDB):** High-performance data transformations and validation of 1M+ rows.
* **Power BI:** * **Power Query:** Professional ETL processing and data shaping.
    * **DAX:** Advanced statistical modeling, segmentation logic, and time-intelligence measures.

---

## 🚀 Key Methodologies

### 🔹 Feature Engineering
To move beyond raw data, I developed several key metrics to drive the analysis:
* **Cancellation Flag:** Derived from `InvoiceNo` (identifying 'C' prefixes) to isolate lost revenue.
* **Risk–Value Segmentation:** A custom logic combining order frequency and cancellation rates to categorize customers into risk tiers.
* **Revenue Metrics:** Calculated total spend per line item ($Quantity \times UnitPrice$) to quantify the financial impact of returns.

### 🔹 Data Modeling
I implemented a **Star Schema** within Power BI to ensure optimal performance and scalability.


---

## 🧼 Data Quality & ETL (Preprocessing)

The raw **Online Retail II** dataset required significant cleaning to ensure analytical integrity. Below are the key data quality issues identified and the specific actions taken to resolve them:

### 🔍 Data Challenges & Resolutions

* **Revenue Integrity:** * *Issue:* Identified non-revenue transactions (`UnitPrice = 0`) and negative quantities (returns/errors).
    * *Action:* Excluded zero-price items from financial calculations and isolated negative quantities using a **Cancellation Flag** for separate analysis.
* **Customer Identification:** * *Issue:* Significant volume of anonymous customers (missing `CustomerID`).
    * *Action:* Removed anonymous records for customer-level segmentation (Tenure/Risk) while retaining them for overall product-level trend analysis.
* **Data Inconsistency:** * *Issue:* Inconsistent SKU codes (one `StockCode` with multiple descriptions) and customers associated with multiple countries.
    * *Action:* Standardized stock descriptions and customer residences by using the **most recent** recorded value in the dataset.
* **Segment Distortion:** * *Issue:* Detected extreme bulk transactions indicating wholesale behavior.
    * *Action:* Flagged these as **Wholesale** to prevent them from skewing **Retail** customer averages.

### ⚙️ Technical Transformations
To optimize the model for Power BI and performance:
1.  **Date Dimension:** Built a specialized calendar table to support Time-Series analysis.
2.  **Star Schema Optimization:** Transformed flat transaction data into a clean Star Schema for faster DAX query performance.

---

## 📈 Analytical Approach

### 1️⃣ Risk–Value Customer Segmentation
Customers were segmented using:
- **Value:** Total Orders per Customer  
- **Risk:** Cancellation Rate per Customer  

Population averages were used as thresholds to define four segments:
- High Value – High Risk  
- High Value – Low Risk  
- Low Value – High Risk  
- Low Value – Low Risk  

This segmentation enables prioritization of customers with the highest business impact.

---

### 2️⃣ Gap Analysis
A comparison between segments revealed:
- **Low-Risk cancellation rate:** ~6%  
- **High-Risk cancellation rate:** ~38%  
- **Gap:** ~32 percentage points  

This gap highlights a significant opportunity for targeted intervention.

---

### 3️⃣ Tenure-Based Analysis
Customers were grouped into tenure buckets to assess whether cancellations were driven by:
- Early onboarding friction
- Long-term dissatisfaction

This provided lifecycle context to customer cancellation behavior.

---

### 4️⃣ Product-Level Revenue Leakage
- Identified **Top 10 products** contributing most to lost revenue using a treemap.
- Compared **cancellation rate vs total orders** at the product level.
  
---

### 5️⃣ Time-Series Analysis
Monthly trends were analyzed to identify:
- Spikes in cancellations
- Seasonal patterns
- Behavioral shifts over time

---

## 📊 Power BI Dashboards

The project features a multi-page interactive report designed for both high-level executive review and deep-dive operational analysis.

### 1. Executive Overview
This dashboard provides a "pulse" on the business, focusing on profitability and customer loyalty:

* **Executive KPIs:**
    * **Total Revenue:** Gross sales across the 2-year period.
    * **Revenue per Customer:** An indicator of individual customer value.
    * **Retention Rate:** The percentage of customers from the previous year who made a successful purchase in the current year, measuring annual loyalty.
    * **AOV (Average Order Value):** Insights into purchasing power and basket size.
* **Key Volume Metrics:** Total distinct **Orders** and unique **Customers** served.
* **Time-Series Analysis:** A dynamic view of **Revenue, Order Volume, and Customer Count** over time to identify seasonal trends and growth patterns.


## 👥 Dashboard 2: Customer Revenue & Retention

This page focuses on behavioral segmentation and high-value customer analysis to identify loyalty patterns and revenue concentration.

### 📈 Customer Value & Activity Metrics
* **Top 10% Revenue Contribution:** A Pareto-style metric showing the percentage of total revenue generated by the top 10% of the customer base.
* **Rolling 12-Month Active Customers:** A dynamic count of customers who made at least one purchase in the last 12 months.
* **One-Time vs. Repeat Buyers:** A donut chart visualizing the ratio of single-purchase users to loyal, recurring customers.

### 📊 Behavioral Analysis
* **Top 15 Customers by Revenue:** A ranked bar chart identifying the most impactful individual accounts.
* **Tenure-Based Recency:** Tracks the time elapsed since a customer's last purchase relative to their first interaction. This provides a score to identify customers who are potentially drifting toward churn.
* **Order Frequency Distribution:** A detailed matrix showing the number and percentage of customers categorized by their total order count.


## 🔍 Dashboard 3: Root Cause Analysis (Cancellations)

This dashboard serves as a diagnostic tool to isolate the financial impact of cancellations and identify high-risk customer segments.

### 🚩 Key Risk Metrics
* **Customer Attrition %:** Percentage of the customer base with at least one cancellation.
* **Lost Revenue:** Total financial impact of cancelled transactions.
* **High-Risk/High-Value Rate:** Specific cancellation rate for top-tier customers, identifying the most critical revenue threats.

### 📉 Risk Mapping & Trends
* **The Risk Matrix (Scatter Plot):** A multidimensional view plotting **Cancellation Rate** against **Total Orders**, with **Tenure Duration** as a legend.
* **Attrition Timeline:** A dual-axis line chart tracking **Cancelled Orders** and **Cancellation Rate** month-over-month to identify seasonal spikes or operational failures.
* **Product Loss Treemap:** A visual hierarchy of the **Top 10 Products** by revenue loss, paired with their cancellation rates to pinpoint "faulty" stock.

### 📋 Deep-Dive Matrices
* **High-Value At-Risk Customers:** A detailed matrix listing the specific accounts that contribute high revenue but show rising cancellation patterns.
* **Product Diagnostic Table:** A granular breakdown of every product’s total orders vs. its cancellation rate.

---

## 💡 Key Insights
- A small segment of **high-value, high-risk customers** accounts for a disproportionate share of revenue loss
- Cancellation behavior varies significantly by **customer tenure**
- A limited number of products drive the majority of **revenue leakage**

---

## 🚀 Business Recommendations
- Prioritize **high-value, high-risk customers** for targeted re-engagement.
- Improve customer experience for short-tenure customers with elevated cancellation rates.
- Investigate product-level issues for Products with high cancellation-to-order ratios.

Scenario analysis suggests that a **12% relative reduction in cancellation rate** among high-risk customers could recover approximately **$32K in revenue**.

---

## 📌 Project Status
✅ Completed  

---

## 👤 Author
**Nabil**  
Data Analyst | Power BI | Python | SQL  

