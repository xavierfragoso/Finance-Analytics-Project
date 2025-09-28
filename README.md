# Finance Analytics Project

## Tools Used
- MySQL Workbench
- CSV dataset
- Tableau

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
    END AS Above_Avg_PE
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
> This query identifies which stocks in each sector have a PE ratio or dividend yield above their sector averages. Focusing on these stocks helps investors and analysts spot potentially overvalued or undervalued securities, benchmark performance within sectors, and make informed portfolio or investment decisions. Highlighting above-average stocks provides actionable insights for sector allocation, risk assessment, and investment strategy.
