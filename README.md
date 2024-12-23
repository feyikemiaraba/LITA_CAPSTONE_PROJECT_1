# Sales Performance Analysis for a Retail Store

## Table of Content

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Explorating Data Analysis](#explorating-data-analysis)

[Data Analysis](#data-analysis)

[Visualization and Analyzation](#visualization-and-analyzation)

### Project Overview
---

In this project, I analyzed the sales performance of a retail store based on the products sold across various regions in 2023 & 2024 using Excel, SQL and Power BI to draw interesting insights and to give a sum up of the data.

<img width="594" alt="2024-11-17 (2)" src="https://github.com/user-attachments/assets/0be686c3-5ab4-4ded-854f-311f50dc0ebf">

<img width="472" alt="2024-11-17" src="https://github.com/user-attachments/assets/a98203d7-747f-4fc9-97bd-491bb046159b">



### Data Sources
---

This Sales Data was gotten from The Incubatot Hub(LITA- Data analysis bootcamp)

### Tools Used
---

- Microsoft Excel - for data cleaning
  - [download here](https://microsoft.com)
- SQL Server - for data analysis
  - [download here](https://microsoft.com)
- PowerBI - for data visualization 
  - [download here](https://microsoft.com)

### Explorating Data Analysis
---

This involved exploring the sales data to answer key questions such as:

- Retrieve the total sales for each product category.
- Find the number of sales transactions in each region.
- Find the highest-selling product by total sales value.
- Calculate total revenue per product.
- Calculate monthly sales totals for the current year.
- Find the top 5 customers by total purchase amount.
- Calculate the percentage of total sales contributed by each region.
- Identify products with no sales in the last quarter.

### Data Analysis 
---

Includes some exciting codes worked with on this project;

```sql server
select * from [dbo].[LITACAPSTONEPROJECT]

----------Total Sales for Each Product Category----------
SELECT Product,
SUM(TotalSales) AS TotalSales
FROM [dbo].[LITACAPSTONEPROJECT]
GROUP BY Product
ORDER by TotalSales asc

-----------Number of Sales Transactions in Each Region-----------
SELECT Region, COUNT(*) AS NumberOfTransactions
FROM [dbo].[LITACAPSTONEPROJECT]
GROUP BY Region
ORDER by NumberOfTransactions asc

----------Highest-Selling Product by Total Sales Value---------
SELECT
TOP 1 Product, 
SUM(TotalSales) AS TotalSales
FROM [dbo].[LITACAPSTONEPROJECT]
GROUP BY Product
ORDER BY TotalSales desc

---------Total Revenue per Product-------
SELECT Product, 
SUM(TotalSales) AS TotalRevenue
FROM [dbo].[LITACAPSTONEPROJECT]
GROUP BY Product
ORDER BY TotalRevenue asc

---------Monthly Sales Totals for the Current Year-------------
SELECT MONTH(OrderDate) AS Month, 
SUM(TotalSales) AS MonthlySales
FROM [dbo].[LITACAPSTONEPROJECT]
WHERE YEAR(OrderDate) = YEAR(GETDATE())  -- Using GETDATE() for the current date in SQL Server
GROUP BY MONTH(OrderDate)
ORDER By Month desc

-----------Top 5 Customers by Total Purchase Amount----------
SELECT Top 5 Customer_Id, 
SUM(TotalSales) AS TotalPurchaseAmount
FROM [dbo].[LITACAPSTONEPROJECT]
GROUP BY Customer_Id
ORDER BY TotalPurchaseAmount DESC

-------------Percentage of Total Sales Contributed by Each Region-------------
WITH TotalSales AS (
SELECT SUM(TotalSales) AS Total
FROM [dbo].[LITACAPSTONEPROJECT]
)
SELECT Region, 
SUM(TotalSales) AS RegionSales, 
(SUM(TotalSales) / (SELECT Total FROM TotalSales)) * 100 AS PercentageOfTotalSales
FROM [dbo].[LITACAPSTONEPROJECT]
GROUP BY Region

	---------Products with No Sales in the Last Quarter----------
SELECT 
DISTINCT S.Product
FROM [dbo].[LITACAPSTONEPROJECT] AS S  -- Your sales data table
WHERE S.Product NOT IN (
SELECT 
DISTINCT S2.Product
FROM [dbo].[LITACAPSTONEPROJECT] AS S2 
WHERE S2.OrderDate >= DATEADD(MONTH, -3, GETDATE())  
    )
```

### Visualization and Analyzation
---

PowerBi was used for this visualization. Below are some of the intresting pictorial representation gotten from codes written on sql server; 

#### 1. Sum of TotalSales by Product
In the diagram below, it shows that SHOES, amongst all other product, is the highest selling product. On the Top 2, we have shoes and Shirt respectively while we have Jacket and Socks at the bottom 2. 

<img width="467" alt="2024-11-17 (3)" src="https://github.com/user-attachments/assets/0facfa14-2bf8-4a98-97fc-a87d4ceb736c">

#### 2. Total Revenue per Product

<img width="390" alt="2024-11-17 (6)" src="https://github.com/user-attachments/assets/e502d517-5180-46bd-8bc6-e21438172605">

#### 3. Number of Sales Transcation in Each Region
<img width="441" alt="2024-11-17 (4)" src="https://github.com/user-attachments/assets/62802300-eba9-4104-8279-ce5585a05af7">

#### 4. Highest Selling Products by TotalSales
<img width="447" alt="2024-11-17 (5)" src="https://github.com/user-attachments/assets/8b852fab-bbfe-4396-a00e-7047b2a15d39">



