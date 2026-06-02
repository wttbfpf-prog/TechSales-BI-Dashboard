# DAX Measures Reference

All custom measures used in the Power BI report, grouped by category.

---

## Core Financials

```dax
Total Revenue = SUM(fact_sales[Revenue])

Total Cost = SUM(fact_sales[Cost])

Total Profit = SUM(fact_sales[Profit])

Total Units = SUM(fact_sales[Units])

Total Orders = DISTINCTCOUNT(fact_sales[OrderID])
```

---

## Profitability

```dax
Gross Margin % =
DIVIDE(
    [Total Profit],
    [Total Revenue],
    0
)

Avg Order Value =
DIVIDE(
    [Total Revenue],
    [Total Orders],
    0
)

Return Rate =
DIVIDE(
    CALCULATE(COUNTROWS(fact_sales), fact_sales[Returned] = 1),
    COUNTROWS(fact_sales),
    0
)
```

---

## Year-over-Year Analysis

```dax
LY Revenue =
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR(dim_date[Date])
)

LY Profit =
CALCULATE(
    [Total Profit],
    SAMEPERIODLASTYEAR(dim_date[Date])
)

YoY Rev Growth % =
DIVIDE(
    [Total Revenue] - [LY Revenue],
    [LY Revenue],
    0
)

YoY Profit Growth % =
DIVIDE(
    [Total Profit] - [LY Profit],
    [LY Profit],
    0
)
```

---

## Time Intelligence

```dax
Cumulative Sales =
CALCULATE(
    [Total Revenue],
    DATESYTD(dim_date[Date])
)

MTD Revenue =
CALCULATE(
    [Total Revenue],
    DATESMTD(dim_date[Date])
)

YTD Revenue =
CALCULATE(
    [Total Revenue],
    DATESYTD(dim_date[Date])
)

YTD Profit =
CALCULATE(
    [Total Profit],
    DATESYTD(dim_date[Date])
)
```

---

## Notes

- All currency measures return values in **Euros (€)**
- `DIVIDE()` is used throughout instead of `/` to handle division-by-zero safely
- Time intelligence measures depend on an active relationship between `fact_sales[OrderDate]` and `dim_date[Date]`
- `SAMEPERIODLASTYEAR` requires a contiguous date table marked as a Date Table in Power BI
