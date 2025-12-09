# Finance Analytics Project

## Tools Used
- MySQL Workbench
- CSV dataset from Kaggle
- Tableau

## Project Overview
Analyzed stock and sector-level financial data to uncover valuation patterns, investor activity, and sector performance trends. Demonstrated intermediate SQL skills including joins, aggregations, and conditional logic, and used Tableau to visualize key insights that support equity analysis, sector comparison, and data-driven investment decisions.

## Key Questions & Insights

### Business Question 1: Which stocks in each sector have a price-to-earnings (PE) ratio above their sector’s average, and which have a dividend yield above their sector’s average?

### SQL Query
```sql
SELECT 
    f.Ticker,
    f.Sector,
    f.PE_Ratio,
    f.Dividend_Yield,
    s.Avg_PE_Ratio,
    s.Avg_Dividend_Yield,
    CASE 
        WHEN f.PE_Ratio > s.Avg_PE_Ratio THEN 'Yes'
        ELSE 'No'
    END AS Above_Avg_PE,
    CASE 
        WHEN f.Dividend_Yield > s.Avg_Dividend_Yield THEN 'Yes'
        ELSE 'No'
    END AS Above_Avg_Dividend
FROM 
    finance f
INNER JOIN 
    sector_avg s
ON 
    f.Sector = s.Sector
ORDER BY 
    f.Sector, f.Ticker;
```

> **Insight:**  
> This analysis compares individual stock metrics to sector averages, highlighting which companies may be overvalued (high P/E) or income-attractive (high dividend yield) relative to their peers. These insights support investment decisions around valuation, risk assessment, and portfolio diversification.

## Tableau Dashboard

View interactive dashboard here: [Stock Valuation & Dividend Yield vs Sector Benchmarks](https://public.tableau.com/app/profile/xavier.fragoso/viz/StockValuationDividendYieldvsSectorBenchmarks/FinanceDashboardValuationYield)

### Business Question 2: Which sectors had the highest average daily trading volume in June and July, and how does this volume vary across months?

### SQL Query
```sql
SELECT
    Sector,
    YEAR(Date) AS year,
    MONTH(Date) AS month,
    AVG(Volume_Traded) AS avg_daily_volume
FROM finance
WHERE MONTH(Date) IN (6,7)
GROUP BY Sector, YEAR(Date), MONTH(Date)
ORDER BY Sector, year, month;
```

> **Insight:**  
> Identifies which sectors saw elevated investor activity and liquidity during June and July. Higher average trading volumes indicate increased market interest, enabling analysts and traders to detect seasonal patterns, sentiment shifts, and high-engagement sectors during mid-year trading.

## Tableau Visualization

View interactive dashboard here: [Avg Daily Volume by Sector (June vs July 2025)](https://public.tableau.com/app/profile/xavier.fragoso/viz/AvgDailyVolumebySectorJuneJuly2025/Dashboard1)
