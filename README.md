# AdventureWorks Profit Analytics – Data Science Project

## 1. Executive Summary

Using the AdventureWorks database, this project follows an end-to-end data analysis workflow to understand the main factors influencing a company’s profit and to forecast future profit.

The project mirrors a realistic business intelligence and data science scenario by combining data transformation, data storage, analytical modelling, and reporting in one pipeline.

AdventureWorks was deployed to a Microsoft SQL Server instance. The database uses a star-style structure centred on the **FactInternetSales** table and supported by multiple dimension tables. Profit was not provided directly in the raw data, so it was calculated using sales revenue, tax amounts, and product costs.

An interactive dashboard was created in **Power BI** to explore profit over time and across geographies, product categories, and subcategories. KPI cards provide an immediate view of performance, while trend and comparison visuals support deeper analysis.

To extend the work beyond historical reporting, **Python** was used for time series forecasting. A **Holt–Winters Exponential Smoothing** model was applied to capture both trend and seasonality and to generate a 12-month forecast. The forecast output was then imported back into Power BI so that historical and forecasted profit values could be analysed together.

---

## 2. Data Infrastructure & Tools

The AdventureWorks database was selected because its schema is clear and well structured, and it represents realistic sales and commercial processes. This provides a strong foundation for demonstrating the full data science workflow.

The database was deployed on a local Microsoft SQL Server instance, which acted as the central data repository. The main tables used were:

- **FactInternetSales**
- **DimCustomer**
- **DimGeography**
- **DimSalesTerritory**
- **DimProduct**
- **DimProductSubcategory**
- **DimProductCategory**
- **DimDate**

Power BI was connected directly to SQL Server to import and model the data. This reflects a typical enterprise analytics setup where a relational database acts as the central source of truth. Power BI was also used to create DAX measures and build interactive visuals.

Python complemented the workflow by enabling time series forecasting. Monthly profit was first prepared in SQL Server and then exported for modelling in Python. In this project, data preparation and business logic were handled within the database, while forecasting was performed in a dedicated analytical environment.

<img width="1281" height="701" alt="Snowflake Schema" src="https://github.com/user-attachments/assets/e5c81766-58f0-45b3-b4f4-b19d53f8bb0b" />

---

## 3. Data Engineering

AdventureWorks is built using a snowflake-style structure around the **FactInternetSales** table, with descriptive attributes provided through dimension tables such as **DimCustomer**, **DimGeography**, **DimSalesTerritory**, **DimProduct**, **DimProductSubcategory**, **DimProductCategory**, and **DimDate**. This structure supports efficient analytical queries and is suitable for reporting and time series analysis.

Data preparation was performed within SQL Server to create an analysis-ready dataset for profit reporting and forecasting. Since profit was not available as a native field, it was derived using:

**Profit = SalesAmount − (TaxAmt + TotalProductCost)**

This calculation was implemented in Power BI as a DAX measure so that profit is recalculated automatically under different filter selections, including time period, geography, and product hierarchy.

For forecasting, profit needed to be represented as a monthly time series. SQL Server was used to aggregate profit by month by joining **FactInternetSales** to **DimDate** and grouping results by calendar year and month. This reduced dataset size and standardised the time granularity before statistical modelling.

The aggregated monthly dataset was then exported to Python for forecasting.

---

## 4. Data Visualisation & Dashboards

Data visualisation was implemented using Power BI to support interactive exploration of profit performance and trends. Power BI was selected due to its integration with SQL Server, support for DAX measures, and ability to combine historical and forecast data within a single model.

The report was designed around a small number of controls and visuals to keep the layout clear while still allowing flexible analysis. Four slicers were used to filter the report by:

- Year  
- Month  
- Product Category  
- Product Subcategory  

Four KPI cards summarise performance under the current filter context:

- Total Sales  
- Tax Paid  
- Total Product Cost  
- Profit  

Trend analysis is supported through two line charts:
- **Profit by Month** (historical trend and seasonality)
- **Profit Forecast (2014)** (forecast generated in Python and imported into Power BI)

Geographical performance is presented using a clustered table showing **profit by country**, enabling comparisons across regions. A detailed table provides a product hierarchy breakdown including **category**, **subcategory**, **number of units sold**, and **profit**.

Overall, the dashboard design supports both high-level monitoring and deeper drill-down analysis across time, geography, and product structure.

<img width="1415" height="799" alt="dashboard" src="https://github.com/user-attachments/assets/6897a227-d233-45a7-851e-615d298e609a" />

---

## 5. Data Analytics

The analytical objective of this project was to forecast short-term profit trends using historical profit derived from the AdventureWorks database. The forecasting task was treated as a **univariate time series problem**, using past monthly profit values to learn patterns and generate forward-looking estimates.

Before modelling, profit was aggregated at a monthly level using SQL Server. This was done by joining **FactInternetSales** with **DimDate** and grouping by calendar year and month. Aggregating at monthly level reduces transaction-level noise and produces a regular time series suitable for forecasting.

The aggregated dataset was then imported into Python for modelling. Although some variable names in the script refer to “sales”, the values represent monthly profit calculated from revenue, tax, and product cost. This is noted to avoid ambiguity and ensure reproducibility.

A **Holt–Winters Exponential Smoothing** model was used to forecast profit. This method is appropriate when the series contains both trend and seasonal structure. The model was configured with:
- Additive trend  
- Additive seasonality  
- Seasonal period = 12 months  

Model performance was evaluated using a train–test split, where the final 12 months were held out as a test set. The model was trained on earlier months and used to forecast the withheld period. Forecast accuracy was measured using **Mean Absolute Percentage Error (MAPE)**.

After evaluation, a final model was trained using the full historical dataset and used to generate a 12-month forecast. The forecasted profit values were exported and imported into Power BI so that historical and predicted values could be visualised together.

![ChatGPT Image Jan 6, 2026, 12_55_27 PM](https://github.com/user-attachments/assets/35557ebc-7983-4704-bc7b-fdce0570149d)
