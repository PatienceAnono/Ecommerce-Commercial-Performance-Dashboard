# Ecommerce Commercial Performance Dashboard

### Power BI | DAX | Data Modeling | Customer Analytics | Cohort Retention | Commercial Intelligence

An end-to-end **Ecommerce Commercial Performance Dashboard** built in Microsoft Power BI to transform transactional ecommerce data into actionable insights across revenue, customers, products, marketing channels, regional performance, and customer retention.

The solution is designed from a **stakeholder-first perspective**, helping commercial, marketing, ecommerce, and management teams understand what is happening in the business, why it is happening, and where opportunities exist.

---

## 📌 Project Overview

Ecommerce businesses generate large volumes of transactional data, but raw sales records do not provide an efficient way for decision-makers to understand commercial performance.

This project transforms transactional ecommerce data into a four-page interactive Power BI analytics solution covering:

- Revenue performance
- Order performance
- Customer acquisition
- Customer retention
- Product performance
- Category performance
- Marketing channel contribution
- Regional performance
- Customer cohorts
- Repeat purchasing behavior

The dashboard combines **data modeling, DAX, time intelligence, customer analytics, cohort analysis, KPI development, and data visualization** into a single business intelligence solution.

---

# 🎯 Business Problem

The business needs a centralized reporting solution that enables stakeholders to quickly answer questions such as:

- How much revenue are we generating?
- Is revenue growing or declining?
- What is our Average Order Value?
- Which products and categories drive the most revenue?
- Which regions generate the highest revenue?
- Which marketing channels contribute to sales?
- How many customers are new versus returning?
- How much revenue comes from returning customers?
- Which customers generate the most value?
- How are customer cohorts retaining over time?
- Which products combine high volume with strong revenue?
- Where are the biggest commercial opportunities?

The dashboard addresses these questions through interactive Power BI reporting.

---

# 🎯 Project Objectives

The primary objectives of the project were to:

1. Build a centralized ecommerce commercial performance dashboard.
2. Track revenue and order performance over time.
3. Monitor key commercial KPIs.
4. Analyze revenue contribution by category.
5. Compare revenue performance across regions.
6. Evaluate marketing channel contribution.
7. Analyze new versus returning customers.
8. Identify high-value customers.
9. Evaluate product and category performance.
10. Analyze product volume versus revenue.
11. Measure repeat purchasing behavior.
12. Analyze customer retention by cohort.
13. Provide stakeholders with an interactive decision-support tool.

---

# 📊 Dataset

The project uses a transactional ecommerce dataset covering **January 2024 through December 2025**.

### Dataset Summary

| Metric | Value |
|---|---:|
| Orders | 5,000 |
| Customers | 501 |
| Products | 10 |
| Categories | 5 |
| Regions | 5 |
| Marketing Channels | 5 |
| Analysis Period | Jan 2024 – Dec 2025 |
| Total Revenue | ~$3.9M |
| Total Quantity | ~14,960 |

### Available Transaction Fields

The dataset contains:

- Order ID
- Order Date
- Customer ID
- Product Name
- Category
- Quantity
- Unit Price
- Revenue
- Region
- Marketing Channel
- Payment Method

Additional analytical fields were created to support customer lifecycle and cohort analysis.

---

# 🧱 Data Modeling

The Power BI solution uses a structured analytical model centered around the ecommerce sales table and a dedicated Date table.

## Core Fact Table

### `Ecommerce_Sales_Dataset_PowerBI`

The primary transactional table contains:

- OrderID
- OrderDate
- CustomerID
- ProductName
- Category
- Quantity
- UnitPrice
- Revenue
- Region
- MarketingChannel
- PaymentMethod

## Date Table

A dedicated `DateTable` was implemented to support reliable time-based analysis.

The Date table is used for:

- Date filtering
- Monthly trend analysis
- Previous month calculations
- Month-over-month analysis
- Time intelligence
- Cohort analysis

The Date table is configured as the official date table for the model.

## Customer & Cohort Fields

Additional analytical fields support customer lifecycle analysis:

- Customer Type
- First Purchase Date
- Cohort Month
- Order Month
- Months Since First Purchase

These fields allow the report to move beyond simple sales reporting into customer behavior and retention analysis.

---

# 🧮 DAX & Business Measures

The dashboard uses DAX to create reusable business metrics and analytical calculations.

Key measures include:

## Revenue & Commercial Metrics

- Total Revenue
- Total Orders
- Total Quantity
- Average Order Value (AOV)
- Previous Month Revenue
- MoM Growth %
- Average Unit Price
- Revenue per Unit

## Customer Metrics

- Total Customers
- New Customers
- Returning Customers
- Repeat Rate %
- Average Revenue per Customer
- Orders per Customer

## Product Metrics

- Product Count
- Product Rank
- Revenue per Unit
- Product revenue contribution

## Cohort & Retention Metrics

- Cohort Size
- Retention %
- Customer retention by months since first purchase
- New Customer Cohort Size

---

# ⏱️ Time Intelligence

Time intelligence was implemented using the dedicated Date table.

This allows the dashboard to analyze:

- Monthly revenue
- Previous month revenue
- Month-over-month growth
- Customer acquisition trends
- Category revenue trends
- Cohort months
- Retention periods

### Example: Previous Month Revenue

```DAX
Previous Month Revenue =
CALCULATE(
    [Total Revenue],
    DATEADD(
        DateTable[Date],
        -1,
        MONTH
    )
)