# AdventureWorks Profit Analytics – Data Science Project

## 1. Executive Summary

Using the Adventure Works database , the analysis involves an examination of the entire data analysis process in order to establish which factors affect a company's profit margins, with further consideration given to forecasting future profits.

The project involves various elements which are seen in real life data analysis projects, such as:

- data manipulation  
- data storage  
- data model  
- the generation of reports from the data  

The primary database, Adventure Works, was installed on a Microsoft SQL Server . The database employs a star schema configuration which centers on the fact table, 'Fact_Internet_Sales', with supporting dimension tables. Since profit was not explicitly given in the raw data, it was calculated by taking the product of sales revenue, product costs and taxes.

The interactive analysis tool has been created using Power BI , which enables users to explore and understand the business profits over different periods, and across various geographical areas, product types and sub-types. Instant visualisation of key performance indicators offers a prompt assessment of the firm's financial performance. Trend and comparative graphics are helpful in more detailed analytical examination.

Using Python for analysis that extends beyond the historical events being reported, a time series forecasting method was employed. An Holt-Winters Exponential Smoothing model was utilised to both capture and forecast both the trend and seasonality of future profits over a twelve month period. The historical forecast data was then re-imported into the Power BI dashboard, allowing users to see actual historical data in conjunction with the projected results.

---

## 2. Data Infrastructure & Tools

The Adventure Works database has been selected due to its snowflake schema being clear and well structured, and it represents real sales and commercial processes. This complete analytical workflow provides a strong foundation for demonstrating the entire data science process.

The central data repository for the project was a local Microsoft SQL Server instance which had the database deployed on it. The tables used in the data analysis were:

- **FactInternetSales**
- **DimCustomer**
- **DimGeography**
- **DimSalesTerritory**
- **DimProduct**
- **DimProductSubcategory**
- **DimProductCategory**
- **DimDate**

Direct links to SQL Server were used in Power BI to bring the data into the software.

The scenario typically describes an enterprise analytics setup with a relational database acting as the central data repository. The use of Power BI greatly streamlined data modelling and the creation of DAX expressions which form measures. Additionally, it allowed for the easy production of interactive dashboards featuring visualisations.

The analysis was complemented by Python, in order to extend it through time series forecasting techniques. The data for monthly profits was first processed within SQL Server before being transferred to a Python script for further processing. In this project, data processing and business logic were encapsulated within the database. Advanced analysis was completed in a separate data analysis platform.

Caption: Adventure Works Snowflake Schema
<img width="1281" height="701" alt="Snowflake Schema" src="https://github.com/user-attachments/assets/cedcfce6-e856-4b5b-8d2b-d30819415d0f" />

---

## 3. Data Engineering

The database of AdventureWorks is built on a snowflake schema. The central fact table is FactInternetSales, while descriptive information is provided by several dimension tables, including DimCustomer, DimGeography, DimSalesTerritory, DimProductSubcategory, DimProductCategory, DimProduct and DimDate.

It possesses capabilities which allow for the efficient running of analytical queries and is ideally suited for time series analysis and for reporting.

Within a database server these activities took place. The purpose was the creation of a useful database for forecasting business profits.

Since profit was not something that could be directly taken from the available data, we had to generate it by using the relationship:

- **Profit = SalesAmount − (TaxAmt + TotalProductCost)**

Using Power BI's DAX formula, this was developed to automatically recalculate the profit based on the selection made from filters such as:

- geographical region  
- time frame  
- product type  

For the purposes of forecasting, monthly profit levels were required.

By utilising SQL Server the monthly time series was produced by aggregating sales data; this involved the use of:

- a join between FactInternetSales and DimDate  
- grouping by calendar year and month  

Aggregated data lowered the data set's size and standardised the time frame for analysis before further statistical analysis took place.

Further analysis of the data was carried out by exporting it to a Python programme for further processing and forecasting.

Caption: Aggregating sales data in SQL server
![ChatGPT Image Jan 6, 2026, 04_11_11 PM](https://github.com/user-attachments/assets/095dd3a9-36d5-4215-a13c-3150a5664322)

---

## 4. Data Visualisation & Dashboards

Data visualisation was implemented using Power BI to support interactive exploration of profit performance and trends within the AdventureWorks dataset.

Power BI was selected due to:

- native integration with SQL Server  
- support for DAX measures  
- ability to combine historical and forecast data within a single semantic model  

The report was designed around a small number of core controls and visuals to maintain clarity while allowing flexible analysis.

Four slicers were implemented to filter the dashboard by:

- year  
- month  
- product category  
- product subcategory  

These slicers enable users to dynamically adjust the scope of analysis and observe how profit metrics respond across different time periods and product hierarchies.

Key performance indicators are displayed using four card visuals:

- total sales  
- tax paid  
- total product cost  
- profit  

These KPIs provide an immediate quantitative summary of business performance under the current filter context.

Profit is calculated using a DAX measure derived from the underlying fact table, ensuring consistency across all visuals.

Trend analysis is supported through two line charts:

1. The first visualises historical profit by month, allowing seasonal patterns and long-term trends to be identified.  
2. The second line chart presents the forecasted profit values for 2014, which were generated externally in Python and imported into Power BI.  

Displaying historical and forecast data together enables direct visual comparison and supports forward-looking analysis.

Geographical performance is analysed using a clustered table that presents profit by country, enabling comparison across sales regions.

In addition, a detailed table visual provides a breakdown by product category and subcategory, including:

- the number of units sold  
- total profit  

This combination of high-level summaries and detailed breakdowns allows both strategic overview and granular analysis within the same dashboard.

Overall, the dashboard design prioritises analytical usability, enabling users to identify trends, compare performance across dimensions, and interpret forecast outputs efficiently.

Caption: Adventure Works Profit Dashboard
<img width="1415" height="799" alt="dashboard" src="https://github.com/user-attachments/assets/5b9d6f35-fcd6-4f70-b98a-1d1ba8e22f10" />

---

## 5. Data Analytics

The analytical objective of the Data Science Project was to forecast short-term profit trends using historical data derived from the AdventureWorks database .

Profit forecasting was formulated as a univariate time series problem, where past monthly profit values were analysed to identify underlying trend and seasonal patterns and to generate forward-looking estimates.

Prior to modelling, profit data was aggregated at a monthly level using SQL Server.

Aggregation was performed by:

- joining the FactInternetSales table with the DimDate table  
- grouping by calendar year and month  

This transformation reduced transactional-level noise and produced a regular, evenly spaced time series, which is a prerequisite for reliable time series forecasting.

The aggregated dataset was then imported into Python  for analytical modelling.

Although variable names within the Python environment reference sales, the values represent monthly profit calculated from sales revenue, tax amounts, and total product costs.

This distinction is documented to ensure clarity and reproducibility.

A Holt–Winters Exponential Smoothing model was selected for forecasting.

This approach is well suited to time series data that exhibits:

- trend  
- seasonality  

Model performance was evaluated using a train–test split, where the final twelve months of data were reserved as a test set.

Forecast accuracy was assessed using:

- Mean Absolute Percentage Error (MAPE)

Following evaluation, a final Holt–Winters model was trained using the full historical dataset and used to generate a twelve-month profit forecast.

The forecasted values were:

- exported  
- integrated into Power BI  
- visualised alongside historical profit trends  

This integration enables direct comparison between observed and predicted values and supports forward-looking analytical insights.

Caption: Adventure Works Forecast Profit Python Code
![ChatGPT Image Jan 6, 2026, 12_55_27 PM](https://github.com/user-attachments/assets/0821deee-0216-4763-aee4-e2ae9900ffd8)
