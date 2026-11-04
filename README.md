# Retail Sales & Delivery Performance Analytics

### End-to-End Business Intelligence Project | Power BI, DAX & Data Analytics

## Project Overview

This project presents an interactive Business Intelligence solution developed using **Microsoft Power BI** to analyze retail sales, profitability, delivery performance, and operational efficiency.

The objective is to transform transactional data into actionable business insights through data modeling, DAX calculations, and interactive dashboards.

The analysis is based on a **synthetic retail dataset covering 2023–2025**, allowing the demonstration of practical data analytics and business intelligence techniques.

## Tools & Technologies

- **Microsoft Power BI Desktop** — Interactive dashboards and business reporting
- **DAX (Data Analysis Expressions)** — Measures, calculated columns, and time intelligence
- **Power Query** — Data cleaning, transformation, and data type management
- **Data Modeling** — Relationships and calendar tables
- **Data Visualization** — KPI cards, trend analysis, matrices, and interactive filters

## Dashboard 1 — Sales Performance Overview

![Sales Performance Dashboard](screenshots/01_sales_overview.png)

This dashboard provides a comprehensive overview of sales and profitability.

**Key features:**
- Total revenue, gross profit, and gross margin KPIs
- Monthly revenue trends from 2023 to 2025
- Profitability analysis by product category
- Interactive filtering by year and product category

**Key results:**
- Total Revenue: **€2.82M**
- Gross Profit: **€915.60K**
- Gross Margin: **32.47%**

The analysis highlights Bikes as the largest contributor to total gross profit.

## Dashboard 2 — Delivery Performance Overview

![Delivery Performance Dashboard](screenshots/02_delivery_performance.png)

This dashboard evaluates operational efficiency and delivery reliability.

**Key features:**
- Total order volume
- Average delivery time
- On-time delivery percentage
- Number of delayed orders
- Quarterly delivery performance trends
- Delivery performance comparison across countries

**Key results:**
- Total Orders: **4,500**
- Average Delivery Time: **5.55 days**
- On-Time Delivery Rate: **83.5%**
- Late Orders: **742**

The dashboard identifies differences in delivery reliability across countries and periods, supporting operational performance monitoring.

## Dashboard 3 — Business Insights & Strategic Analysis

![Business Insights Dashboard](screenshots/03_business_insights.png)

The third dashboard combines financial and operational indicators to support strategic decision-making.

**Key features:**
- Revenue associated with delayed deliveries
- Percentage of revenue associated with late orders
- Country-level profitability and delivery performance matrix
- Revenue from delayed orders by product category
- Interactive geographical and product filters

**Key results:**
- Revenue Associated with Late Orders: **€473.48K**
- Revenue in Late Orders: **16.79% of total revenue**
- France has the highest percentage of revenue associated with delayed orders (**18.17%**).
- Spain achieves the highest on-time delivery rate (**85.5%**).
- Bikes represents the largest product category by revenue associated with delayed orders.

## Business Insights & Recommendations

**1. Monitor revenue exposure to delivery delays**

Approximately 16.79% of total revenue is associated with delayed orders. Monitoring this KPI can help prioritize operational improvements and customer experience initiatives.

**2. Investigate regional delivery performance**

France shows a relatively high proportion of revenue associated with delayed deliveries, while Spain demonstrates stronger delivery reliability. A comparison of regional logistics processes could identify opportunities for improvement.

**3. Prioritize high-value product categories**

Bikes generates the largest absolute revenue associated with delayed deliveries. Further analysis of delay rates, order volumes, and fulfillment processes could help identify the underlying operational drivers.

These findings are descriptive and do not establish causal relationships.

## Data Modeling & DAX

The analytical model uses a dedicated calendar table connected to sales transactions through the order date, enabling time-based reporting.

The project includes DAX calculations using:

- `CALCULATE()` — Filter context manipulation
- `DISTINCTCOUNT()` — Unique order counting
- `AVERAGEX()` — Average delivery time at order level
- `DATEDIFF()` — Delivery duration calculations
- `DIVIDE()` — Safe percentage calculations
- `YEAR()` and `QUARTER()` — Date-based analysis

### Example DAX Measures

**Gross Profit**

```dax
Gross Profit =
SUM(Sales[LinePrice]) - SUM(Sales[LineCost])
```

**Gross Margin**

```dax
Gross Margin % =
DIVIDE([Gross Profit], [Total Revenue], 0)
```

**On-Time Delivery Rate**

```dax
On-Time Delivery % =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(Sales[OrderID]),
        Sales[IsOnTime] = TRUE()
    ),
    [Order Count],
    0
)
```

**Revenue Associated with Late Orders**

```dax
Late-Order Revenue =
CALCULATE(
    [Total Revenue],
    Sales[IsOnTime] = FALSE()
)
```

## Repository Structure

```text
Retail-Sales-Delivery-Analytics/
│
├── Retail_Sales_Delivery_Analytics.pbix
├── README.md
│
├── data/
│   └── retail_sales_synthetic.csv
│
└── screenshots/
    ├── 01_sales_overview.png
    ├── 02_delivery_performance.png
    └── 03_business_insights.png
```

## How to Explore the Project

1. Download or clone this repository.
2. Open the `.pbix` file using Microsoft Power BI Desktop.
3. If necessary, update the CSV source path in Power Query to point to the local file in `data/`.
4. Explore the three report pages using the interactive filters.
5. Analyze financial and operational KPIs across different years, countries, and product categories.

## Skills Demonstrated

This project demonstrates practical experience in:

- Data cleaning and transformation
- Relational data modeling
- DAX measure development
- KPI definition and monitoring
- Time-series analysis
- Financial and operational analytics
- Interactive dashboard design
- Data storytelling and business insight generation

## Data Disclaimer

This project uses **synthetically generated data** for educational and portfolio purposes. The results do not represent the financial or operational performance of a real company.

The project was developed independently to apply and extend Power BI and DAX skills acquired through data analytics training.

---

**Developed as a personal Data Analytics & Business Intelligence portfolio project.**
