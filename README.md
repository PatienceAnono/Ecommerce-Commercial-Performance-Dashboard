# Ecommerce Commercial Performance Dashboard (Power BI)

## Overview

This project is an end-to-end Commercial Performance Dashboard built in Power BI to analyze ecommerce sales data across revenue performance, customer behavior, product trends and regional contribution.

The objective of this dashboard is to move beyond basic reporting and deliver clear, actionable insights that support strategic business decisions.

---

## Business Questions Addressed

- How is revenue trending month over month?
- Which products and categories drive the most revenue?
- Are we experiencing positive or negative MoM growth?
- What is the revenue contribution of new vs returning customers?
- Which regions generate the highest commercial value?
- Is revenue concentrated in a small number of products?

---

## Key Metrics

- Total Revenue
- Total Orders
- Total Customers
- Average Order Value (AOV)
- Previous Month Revenue
- MoM Growth %
- Repeat Rate %
- Revenue by Category
- Revenue by Customer Type
- Top 10 Products by Revenue
- Revenue by Region

---

## 📊 Dashboard Preview

### Revenue Overview
[![Revenue Overview](Images/Revenue%20Overview.png)](Images/Revenue%20Overview.png)

### Product Performance
[![Product Performance](Images/Product%20Performance.png)](Images/Product%20Performance.png)

### Customer Insights
[![Customer Insights](Images/Customer%20Insights.png)](Images/Customer%20Insights.png)

### 1. Revenue Overview
- KPI summary cards (Revenue, Orders, Customers, AOV)
- Monthly revenue trend (Year-Month analysis)
- Revenue by category
- Revenue by region
- MoM Growth indicator
- Interactive date and region slicers

### 2. Product Performance
- Top 10 products by revenue
- Revenue and quantity comparison
- Category revenue trends over time
- Revenue vs Quantity scatter analysis

### 3. Customer Insights
- Customer Type Distribution (New vs Returning)
- Customer revenue contribution
- Revenue by customer segment
- Repeat Rate %
- Customer summary table

---

## Data Modeling Approach

The report follows a structured star schema design:

- Dedicated Date Table
- One-to-many relationship between Date and Sales tables
- Marked Date table for proper time intelligence
- Clean DAX-based calculations for performance metrics

Time intelligence functions used:
- DATEADD
- TOTALYTD
- MoM calculations

This ensures accurate filtering, scalable modeling and reliable commercial analysis.

---

## Sample DAX Measures

Previous Month Revenue:
CALCULATE(
    [Total Revenue],
    DATEADD(DateTable[Date], -1, MONTH)
)

MoM Growth %:
DIVIDE(
    [Total Revenue] - [Previous Month Revenue],
    [Previous Month Revenue]
)

Total Customers:
DISTINCTCOUNT(Ecommerce_Sales_Dataset_PowerBI[CustomerID])

---

## Key Insights

- Revenue shows fluctuating but generally upward momentum.
- Returning customers contribute the majority of revenue.
- A small number of products drive a large share of total revenue.
- Revenue contribution varies significantly by region.
- Customer acquisition is relatively small compared to retention-driven revenue.

---

## Tools Used

- Power BI Desktop
- DAX
- Data Modeling (Star Schema)
- Time Intelligence Functions

---

## How to Use

1. Download the `.pbix` file from this repository.
2. Open in Power BI Desktop.
3. Use slicers (Date and Region) to explore trends.
4. Navigate between dashboard pages for Revenue, Product, and Customer insights.

---

## Project Purpose

This project demonstrates the ability to:

- Build commercial-focused dashboards
- Design clean and scalable data models
- Implement advanced DAX calculations
- Translate business data into actionable insights

It reflects practical business intelligence skills applicable in commercial analytics and data consulting environments.
