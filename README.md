# Finance Analytics Project

## Tools Used
- MySQL Workbench
- CSV dataset from Kaggle
- Tableau

## Project Overview
This project analyzes stock and sector-level financial data to uncover actionable insights for investors and analysts. Using SQL for data querying and Tableau for visualization, the project explores stock valuation metrics and trading activity trends.

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
> Stocks with PE ratios or dividend yields above their sector averages may indicate over or undervaluation. Highlighting these stocks helps investors benchmark performance, assess risk, and optimize portfolio allocation.

## Tableau Dashboard

View dashboard: [PE & Dividend Yields Above Sector Avg](https://public.tableau.com/app/profile/xavier.fragoso/viz/FinancialAnalysisonStocks/PEDividendYieldsAboveSectorAvg)

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
> Sectors with higher average daily trading volumes in June and July show greater investor activity and liquidity, helping traders identify the most actively traded sectors mid-year.

## Tableau Visualization

View visualization: [Avg Daily Volume by Sector (June–July 2025)](https://public.tableau.com/app/profile/xavier.fragoso/viz/AvgDailyVolumebySectorJuneJuly2025/AvgDailyVolumebySectorJuneJuly2025)
