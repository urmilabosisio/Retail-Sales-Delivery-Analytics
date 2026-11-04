# Retail Sales & Delivery Performance Analytics

**An independent Power BI / DAX portfolio project analyzing sales growth, gross profitability and order-level delivery reliability for a fictional European bicycle retailer.**

**Tech stack:** Power BI Desktop · DAX · Data modeling · Time intelligence · Python (data generation / QA)

> **Data notice:** All 7,688 transaction lines and 4,500 orders in this repository are **synthetic**, deterministically generated, and do not belong to a real company. The dashboard and code are an independent demonstration of skills practiced while learning Power BI; the original DataCamp exercise file and dataset are **not** redistributed here.

## What the dashboard answers

1. **Commercial performance:** What is our revenue, gross profit and quarter-over-quarter growth?
2. **Category profitability:** Which product families contribute most to revenue and margin?
3. **Delivery reliability:** How often do we deliver by the promised deadline and how does performance vary by market?

## Preview of computed KPIs

See [`analysis/synthetic_insights.md`](analysis/synthetic_insights.md) for verified values and [`analysis/quarterly_kpis.csv`](analysis/quarterly_kpis.csv) for quarterly metrics. Values are illustrative and **not** real-world business findings.

## Proposed report pages

| Page | Visuals | Decisions supported |
|---|---|---|
| Executive Overview | KPI cards, revenue trend, sales by category, slicers | Growth and performance monitoring |
| Product & Profitability | Profit by category, product matrix, average order value | Product mix and margin review |
| Delivery Operations | On-time rate, order-level lead times, quarterly trend | Delivery reliability prioritization |

## Model

```text
Dates (1) ──── (*) Sales
         Date    OrderDate
```

- `Sales` records **order lines**, not distinct orders.
- `Dates` is a contiguous date dimension generated in DAX.
- Measures use explicit `DISTINCTCOUNT` and order-grain iterators where appropriate.
- Classic DAX time intelligence compares current revenue to the preceding quarter with `DATEADD`.

## Reproduce locally

1. Open **Power BI Desktop** and import [`data/retail_sales_synthetic.csv`](data/retail_sales_synthetic.csv) as `Sales`.
2. Create the calendar from [`dax/01_date_table.dax`](dax/01_date_table.dax) and relate `Dates[Date]` to `Sales[OrderDate]`.
3. Create calculated columns from [`dax/02_sales_calculated_columns.dax`](dax/02_sales_calculated_columns.dax) **one at a time**.
4. Create measures from [`dax/03_measures.dax`](dax/03_measures.dax) **one at a time**.
5. Build the three report pages; complete steps and visual mappings are in the **[Italian Power BI build guide](docs/POWER_BI_GUIDE_IT.md)**.
6. Save your own `Retail_Sales_Delivery_Analytics.pbix` and add it to this repo once ready.

### Rebuild and validate the data (Python 3, no external packages)

```bash
python src/generate_data.py
python src/validate_and_summarize.py
```

The seeded generator guarantees reproducible synthetic examples and the validator checks line uniqueness, monetary arithmetic, order consistency, and date logic.

## Design choices

- **Order-level vs line-level:** An average of `Sales[Order2Delivery]` over rows can overweight orders containing many products. The `Avg Promised Lead Days` measure averages over distinct order IDs instead.
- **Financial honesty:** `Gross Profit` subtracts direct modeled costs only. It is not EBITDA or net income.
- **Temporal correctness:** The date dimension covers full, continuous calendar years; the first quarter in the data has no prior quarter against which to calculate QoQ.
- **No proprietary data:** Public portfolio materials use only independently generated synthetic transactions and original DAX/report design.

## Contents

```text
retail-sales-delivery-powerbi/
├── README.md
├── data/retail_sales_synthetic.csv
├── src/generate_data.py
├── src/validate_and_summarize.py
├── dax/01_date_table.dax
├── dax/02_sales_calculated_columns.dax
├── dax/03_measures.dax
├── analysis/quarterly_kpis.csv
├── analysis/category_kpis.csv
├── analysis/synthetic_insights.md
└── docs/
    ├── POWER_BI_GUIDE_IT.md
    ├── PROJECT_BRIEF.md
    ├── DATA_DICTIONARY.md
    └── QA_CHECKLIST.md
```

## References

- [Microsoft: date table design in Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/model-date-tables)
- [Microsoft: marking a date table](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-date-tables)
- [Microsoft: DATEADD (DAX)](https://learn.microsoft.com/en-us/dax/dateadd-function-dax)

## Author / status

**Portfolio project, version 1.0 — dataset + DAX + reproducibility + build guide completed.** A native `.pbix` built with these files and dashboard screenshots can be added after completing the Power BI Desktop instructions. Dataset and source code in this repository are original examples created for learning and demonstration.
