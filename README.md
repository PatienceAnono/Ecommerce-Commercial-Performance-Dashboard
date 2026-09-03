# Ecommerce Commercial Performance Dashboard

### Power BI · DAX · Data Modeling · Customer Analytics · Cohort Retention · Commercial Intelligence

An end-to-end **Ecommerce Commercial Performance Dashboard** built in Microsoft Power BI to transform raw transactional ecommerce data into decision-ready insight across revenue, customers, products, marketing channels, regional performance, and customer retention.

Built by **PA Data Analytics** from a stakeholder-first perspective — designed for business owners, ecommerce managers, marketing managers, commercial teams, and senior management, not just analysts.

---

## 📌 Project Overview

Ecommerce businesses generate large volumes of transactional data, but raw sales records don't give decision-makers an efficient way to understand commercial performance. This project turns two years of transactional ecommerce data into a four-page interactive Power BI analytics solution covering:

- Revenue and order performance
- Customer acquisition and retention
- Product and category performance
- Marketing channel and regional contribution
- Cohort-based repeat purchasing behavior

The solution combines **data modeling, DAX, time intelligence, customer analytics, cohort analysis, KPI development, and data visualization** into a single business intelligence deliverable — built to withstand the kind of scrutiny a paying client or senior stakeholder would apply.

---

## 🎯 Business Problem

The business needed a centralized reporting solution that lets stakeholders quickly answer:

- How much revenue are we generating, and is it growing or declining?
- What is our Average Order Value?
- Which products and categories drive the most revenue?
- Which regions and marketing channels generate the highest revenue?
- How many customers are new versus returning, and how much revenue comes from each?
- Which customers generate the most value?
- Are we actually retaining customers, and which cohorts retain best?
- Where are the biggest commercial opportunities — and risks?

---

## 🎯 Project Objectives

1. Build a centralized ecommerce commercial performance dashboard
2. Track revenue and order performance over time
3. Monitor key commercial KPIs with correct, presentation-ready formatting
4. Analyze revenue contribution by category and region
5. Evaluate marketing channel and payment method contribution
6. Analyze new versus returning customers on a **time-bound** basis, not a lifetime one
7. Identify high-value customers and products
8. Analyze product volume versus revenue relationships
9. Measure repeat purchasing behavior
10. Analyze customer retention by acquisition cohort
11. Deliver an interactive, decision-support tool — not just a data display

---

## 📊 Dataset

Transactional ecommerce data covering **January 2024 – December 2025**.

| Metric | Value |
|---|---:|
| Orders | 5,000 |
| Customers | 501 |
| Products | 10 |
| Categories | 5 |
| Regions | 5 |
| Marketing Channels | 5 |
| Payment Methods | 4 |
| Analysis Period | Jan 2024 – Dec 2025 |
| Total Revenue | $3,900,365 |
| Total Quantity Sold | 14,960 units |
| Average Order Value | $780 |

### Transaction Fields

`OrderID` · `OrderDate` · `CustomerID` · `ProductName` · `Category` · `Quantity` · `UnitPrice` · `Revenue` · `Region` · `MarketingChannel` · `PaymentMethod`

Additional analytical fields were engineered to support customer lifecycle and cohort analysis (see below).

---

## 🧱 Data Modeling

### Core Fact Table — `Ecommerce_Sales_Dataset_PowerBI`

The primary transactional table, at one row per order line.

### Customer & Cohort Fields

Calculated columns supporting lifecycle and cohort analysis:

- **`First Purchase Date`** — each customer's earliest order date
- **`Cohort Month`** — the month a customer was acquired (`First Purchase Date` truncated to month)
- **`Months Since First Purchase`** — elapsed months between a given order and that customer's first purchase, per order
- **`Customer Type`** — a lifetime purchase-count classification (see *Design Decisions* below for an important caveat on this field)

---

## 🧮 DAX & Business Measures

### Revenue & Commercial Metrics

| Measure | Logic |
|---|---|
| `Total Revenue` | `SUM(Revenue)` |
| `Total Orders` | Distinct order count |
| `Total Quantity` | `SUM(Quantity)` |
| `AOV` | `DIVIDE([Total Revenue], [Total Orders])` |
| `Previous Month Revenue` | `CALCULATE([Total Revenue], DATEADD(...,-1,MONTH))` |
| `MoM Growth %` | `DIVIDE([MoM Change], [Previous Month Revenue])` |
| `Revenue per Unit` | `DIVIDE([Total Revenue], [Total Quantity])` |

### Customer Metrics

| Measure | Logic |
|---|---|
| `Total Customers` | Distinct customer count |
| `New Customers` | Distinct customers whose `First Purchase Date` falls **within the currently selected period** |
| `Returning Customers` | Distinct customers active in the period whose `First Purchase Date` predates it |
| `New Customer Revenue` / `Returning Customer Revenue` | Revenue split using the same time-bound logic — plots as two columns in one chart with no need for a separate dimension table |
| `Repeat Rate %` | % of customers with more than one lifetime order |
| `Avg Revenue per Customer` | `DIVIDE([Total Revenue], [Total Customers])` |
| `Orders per Customer` | Lifetime orders per customer, filter-context aware |

### Product Metrics

| Measure | Logic |
|---|---|
| `Product Count` | Distinct product count |
| `Product Rank` | `RANKX` over products by revenue, dense rank |
| `Revenue per Unit` | Product-level price efficiency |

### Cohort & Retention Metrics

| Measure | Logic |
|---|---|
| `Cohort Size` | Distinct customers in the cohort matching the current `Cohort Month` context |
| `Retention %` | Active customers in a given `Months Since First Purchase` ÷ that cohort's `Cohort Size` |

---

## ⏱️ Time Intelligence

**Example — Previous Month Revenue:**

```dax
Previous Month Revenue =
CALCULATE(
    [Total Revenue],
    DATEADD(DateTable[Date], -1, MONTH)
)
```

**Example — time-bound New Customers**, deliberately built without relying on a marked date table relationship, so it responds correctly to whichever date filter is active regardless of relationship path:

```dax
New Customers =
VAR PeriodStart = MIN(Ecommerce_Sales_Dataset_PowerBI[OrderDate])
VAR PeriodEnd   = MAX(Ecommerce_Sales_Dataset_PowerBI[OrderDate])
RETURN
CALCULATE(
    DISTINCTCOUNT(Ecommerce_Sales_Dataset_PowerBI[CustomerID]),
    Ecommerce_Sales_Dataset_PowerBI[First Purchase Date] >= PeriodStart,
    Ecommerce_Sales_Dataset_PowerBI[First Purchase Date] <= PeriodEnd
)
```

---

## 🔍 Key Analytical Findings

This isn't just a dashboard — the model surfaced a real commercial issue worth calling out on its own:

> **Customer acquisition has effectively stopped.** 37% of the entire 501-customer base (187 customers) was acquired in the very first month of the dataset. Acquisition then declined sharply month over month, and **zero new customers were acquired in the final 8 months** of the two-year window (May–Dec 2025). Filtered to 2025 alone, just 5 new customers were acquired against 492 returning — contributing only $21K of the year's $1.99M in revenue.

This is the kind of finding a raw sales table hides and a properly built cohort model surfaces immediately — exactly the value this dashboard is designed to deliver.

---

## 💡 Recommendations

Translating the finding above into action — this is the difference between a dashboard and a decision:

1. **Separate acquisition tracking from revenue tracking by channel.** `Revenue by Marketing Channel` currently shows all five channels within 6% of each other — but that revenue is dominated by the existing 501-customer base, not new signups. Add a `New Customers by Marketing Channel` measure to see whether *any* channel is still acquiring, since the current view can mask a channel that looks healthy on revenue while contributing zero new customers.
2. **Set a standing new-customer-acquisition target and alert threshold.** With acquisition at zero for 8 straight months, this should be a headline KPI on Revenue Overview, not something that only surfaces on the Retention Cohort page.
3. **Investigate whether this is a demand-side or supply-side problem** — i.e., has marketing spend on top-of-funnel channels actually dropped, or has spend continued while conversion has collapsed? The dashboard can show *that* acquisition stopped; closing this loop needs marketing spend data joined in, which isn't currently in this model.
4. **Consider a referral/advocacy push.** `Referral` is already the top-performing channel by revenue — with a 99.8% repeat rate, this customer base is clearly loyal. A structured referral program could convert that loyalty into the new-customer pipeline that's currently missing.
5. **Build a customer value tier** (not currently in the model — e.g., revenue quartiles) to identify which of the 501 existing customers are worth protecting most, given the business currently has no acquisition engine offsetting any future churn.

**Caveat:** these recommendations follow directly from the pattern in the data as modeled. Before acting on them commercially, they'd need to be checked against real marketing spend and campaign records, in case the acquisition drop reflects a change in how new signups were tagged or recorded rather than a genuine stop in acquisition.

---

## 🛠️ Design Decisions & Data Quality Notes

Documenting these because a portfolio project should show judgment, not just output:

- **`Customer Type` is a lifetime classification, not a time-bound one.** It flags a customer as "New" only if they have ever placed exactly one order across the *entire* two-year dataset — which is why it shows 500 of 501 customers as "Returning." This is correct behavior for what it measures, but it cannot answer "how many new customers did we acquire this month," which is why the separate time-bound `New Customers` / `Returning Customers` measures exist alongside it.
- **`Retention %` and `Cohort Size` only make sense inside a proper Cohort Month × Months-Since-First-Purchase matrix.** Evaluated flat (no cohort row context), `Cohort Size` correctly-but-confusingly resolves to whatever the single most recent cohort is — which can be as small as 1 customer. Verified against the full cohort table before shipping, to confirm the measures are correct as designed rather than assuming a flat-query result was representative.
- Two duplicate measures were identified and removed during model audit: `Revenue per Order` (identical to `AOV`) and the original `Customer Revenue` (identical to `Total Revenue` despite its name — since renamed and corrected to `Avg Revenue per Customer`).

---

## 🎨 Brand & Visual System

Built to the PA Data Analytics visual identity:

| Swatch | Hex | Usage |
|---|---|---|
| Primary Navy | `#272D78` | Backgrounds, headers, key shapes |
| Primary Blue | `#3386C7` | Subheads, secondary shapes, default chart color |
| Light Background Grey | `#F8F9FC` | Content backgrounds |
| Dark Text Grey | `#555770` | Body copy |
| Accent Teal | `#2EC4B6` | Single highlight only — never a base color |

---

## 📁 Report Pages

1. **Revenue Overview** — financial performance: revenue, orders, AOV, growth trend, category/region/channel contribution
2. **Customer Insights** — who the customers are, new vs. returning, revenue contribution by customer type, top customers
3. **Product Performance** — top products, category performance, volume-vs-revenue relationship
4. **Retention Cohort** — cohort retention matrix, cohort size by acquisition month, retention trend

---

## 🧰 Tools & Skills Demonstrated

Power BI Desktop · DAX (time intelligence, iterators, filter context manipulation) · Data modeling · Cohort analysis · KPI design · Stakeholder-focused data storytelling · Data quality auditing

---

*Built by [PA Data Analytics](https://padataanalytics.com) — Nairobi-based e-commerce and marketing analytics consultancy.*
