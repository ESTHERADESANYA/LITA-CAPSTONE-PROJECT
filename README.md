# LITA-CAPSTONE-PROJECT

### PROJECT TITLE: SALES PERFORMANCE ANALYSIS
[PROJECT OUTLINE](#PROJECT-OUTLINE)

[PROJECT OVERVIEW](#PROJECT-OVERVIEW)

[PROJECT OBJECTIVE](#PROJECT-OBJECTIVE)

[DATA DESCRIPITION](#DATA-DESCRIPITION)

[DATA TOOLS](#DATA-TOOLS)

### PROJECT OVERVIEW
```
This repository contains the documentation for the Lita Capstone Project,focusing on sales analytics using Excel, SQL and PowerBI.
The project aims to uncover key insights such as top-selling products, regional performance, and monthly sales trends. Additionally,
The goal is to provide insight into average sales per product and total revenue by region, to inform business decisions. 
```

### PROJECT OBJECTIVE:
```
Analyze total sales by product to identify top-selling products and areas for improvement.
Examine sales trends by region to inform geographic expansion strategies.
Investigate monthly sales patterns to optimize inventory management and forecasting.
Calculate average sales per product to identify opportunities for product development.
evaluate total revenue by region to allocate resources effectively 
```

### DATA DESCRIPITION
```
Sales data from January 2023 to August 2024.
Order ID, Customer ID, Product, Region, Order Date, Quantity, Unit Price and Total Sales
Data sources:Excel files.
```

### DATA TOOLS:
```
Microsoft Excel: Data analysis and manipulation
SQL Server: Data storage and quering
PowerBI: Data visualization and reporting
```
### METHODOLOGY:
### Data Collection
```
The dataset for the analysis was provided by LITA Incubator Hub.
```

### EXPLORATORY DATA ANALYSIS (EDA)
1. Data Cleaning and Analysis on Excel:
   1. Data loading and inspection
   2. Checked for Null values and removed duplicates by highligting and using the remove duplicates features.
   3. Utilized Pivot tables to summarize data, Filter to improve data visualization and enhance insights.
   4. Charts to visualize trends and pattern, Slicer for interactive filtering.
       
2. Data Cleaning and Transformation on PowerBI: 
- Used power query editor to clean and transform data.
- Removed duplicates using remove Duplicates feature.
- Changed data types using the data type feature.
- Checked for data consistency using the column quality, column profile, and column distribution.
- Data visualization: created Power BI dashboard that visualizes the insights found in Excel and SQL which include a sales overview, top-performing products, and
regional breakdowns.
(e.g, charts, cards,tables).

3. CALCULATIONS
- calculate metrics such as average sales per product and total revenue by region.

### SQL QUERIES
```
create database Sales_Data_Capstone
--- 1 retrieve the total sales for each product category
Select * from [dbo].[Sales Data]
select sum(total_sales) as Total_Sales,
product from [dbo].[Sales Data]
group by product
order by Total_sales Desc

--2 find the number of sales transactions in each region 
select region,
count(Orderid) 
as Number_of_Sales_Transaction
from [dbo].[Sales Data]
group by region 
order by Number_of_Sales_Transaction desc

----3 find the highest selling product by total sales region
select Top 1
product,
sum(total_sales) as Total_sales_value 
from [dbo].[Sales Data]
group by product 
order by Total_sales_value desc

--4 calculate total revenue per product
select product,
sum(Total_sales) as Total_Revenue
from [dbo].[Sales Data]
group by product
order by Total_Revenue DESC

------- 5 calculate monthly sales totals for the current year
select month(orderdate) as Sales_Month, 
sum(Total_sales) as Monthly_Sales_Total
from [dbo].[Sales Data]
where year(orderdate) = YEAR(getdate())
GROUP BY MONTH(orderdate)
order by Sales_month 

----6 find the top 5 customers by total purchase amount
select Top 5 Customer_ID,
SUM(Total_Sales)
as Total_Purchase_Amount 
from [dbo].[Sales Data]
GROUP BY Customer_Id
Order by Total_Purchase_Amount DESC 

---7 Calculate the percentage of totaltotal sales contributed by each region
Select Region,
Sum(Total_Sales) as Regional_Sales,
Convert (Decimal(5,2),
Round((Cast(Sum(Total_Sales) as 
Decimal(10,2)) / (Select Sum (Total_Sales) 
From [dbo].[Sales Data])) * 100, 2))
as Sales_Percentage 
From [dbo].[Sales Data]
Group by Region
Order by Regional_sales desc
Select * from [dbo].[Sales Data]

----8 Identify products with no sales in the last quarter
Select product
From [dbo].[Sales Data]
Where Product Not in (
Select Product From [dbo].[Sales Data]
Where 
OrderDate >= DATEADD(quarter,-1, Getdate())
)
and OrderDate >= DATEADD(quarter,-1, Getdate()) 
```

### RESULTS
```
TOTAL SALES PER PRODUCT
- Top-Selling Products: Shoes (613,380) and Shirts (485,600) are the highest performers, making up over 50% of total sales.
- Lower-Selling Products: Socks (180,785) and Jackets (208,230) have the weakest sales, indicating possible opportunities for improvement.
- Balanced Sales: Sales are relatively well-distributed across the products, with moderate performance from Gloves (296,900) and Hats (316,195).
- Opportunities: Targeted promotions for socks and jackets, and cross-promotions with top-sellers like shoes and shirts, could help boost overall revenue.

TOTAL SALES PER REGION
- Top-Performing Region: The South region leads with 927,820 in sales, accounting for about 44.2% of total sales.
Other Regions:
- East: 485,925 (23.1% of total sales)
- North: 387,000 (18.4% of total sales)
- West: 300,345 (14.3% of total sales)

TOTAL SALES PER MONTH
- Top Month: February with 546,300, the highest sales.
- Lowest Month: September with 34,720, significantly lower than other months.
- Steady Performers: January, July, and June had relatively strong sales, between 240,000 and 275,000.
- Declining Trend: Sales show a notable drop after February, with most months dipping below 150,000.
```
