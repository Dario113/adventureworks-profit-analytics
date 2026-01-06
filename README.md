# AdventureWorks Profit Analytics – Data Science Project

## 1. Executive Summary

The Data Science Project was undertaken using the AdventureWorks sample database provided by Microsoft. The purpose of the analysis was to examine a complete data workflow in order to identify which factors influence a company’s profit levels and to forecast future profit trends.

The project integrates several elements commonly seen in real business intelligence and data science projects. These include data manipulation, data storage, data modelling, analytical forecasting, and interactive reporting.

The AdventureWorks database was downloaded and deployed to a SQL Server instance. The database follows a star schema design, centred on the FactInternetSales table and supported by multiple dimension tables.

Profit was not explicitly stored in the original dataset and was therefore derived using the relationship:

Profit = SalesAmount − (TaxAmt + TotalProductCost)

This calculation was implemented dynamically within Power BI using DAX.

---

## 2. Data Infrastructure & Tools

The AdventureWorks database was selected due to its clear and well-structured snowflake schema and its representation of realistic sales and commercial processes.

The project was deployed on a Microsoft SQL Server instance, which acted as the central data repository. The tables used for the analysis were:

- DimCustomer  
- DimDate  
- DimGeography  
- DimProduct  
- DimProductCategory  
- DimProductSubcategory  
- DimSalesTerritory  
- FactInternetSales  

Power BI was connected directly to SQL Server to extract and model the dataset. This reflects a typical enterprise analytics scenario where a relational database supports downstream analytical tools.

Python was used to complement the analysis through time series forecasting techniques.

---

## 3. Data Engineering

Data engineering activities focused on preparing AdventureWorks transactional data for analytical workloads.

Transactional data was aggregated into monthly profit observations using SQL Server. This involved joining FactInternetSales with DimDate, grouping records by calendar year and month, and exporting the resulting dataset to CSV.

This aggregation reduced data complexity and ensured a consistent time granularity before forecasting was performed in Python.

---

## 4. Data Visualisation & Dashboards

An interactive dashboard was created using Power BI.

The dashboard contains:
- 4 slicers: Year, Month, Category, Subcategory  
- 4 cards: Total Sales, Tax Paid, Product Cost, Profit  
- 2 line charts:  
  - Profit by Month  
  - Profit Forecast 2014  
- 1 clustered table: Profit by Country  
- 1 detailed table: Category, Sub Category, # Sold, Profit  

The forecasted results produced in Python were imported back into Power BI so that actual historical and forecasted profit results could be analysed together on the dashboard.

---

## 5. Data Analytics

The analysis involved forecasting short-term profit trends using Holt–Winters Exponential Smoothing.

The aggregated dataset was imported into Python and divided into:
- Training data: all months except last 12  
- Test data: final 12 months  

The model was evaluated using Mean Absolute Percentage Error (MAPE).

After validation, a final model was trained on the full dataset and used to generate twelve-month forward forecasts. The forecasted values were exported and visualised in Power BI.

---

## References

- Microsoft (2024) AdventureWorks sample databases  
- Microsoft (2024) SQL Server documentation  
- Microsoft (2024) Power BI documentation  
- Microsoft (2024) DAX overview  
- Hyndman, R.J. and Athanasopoulos, G. (2021) Forecasting: Principles and Practice  
