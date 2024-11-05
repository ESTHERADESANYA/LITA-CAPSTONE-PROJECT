# LITA-CAPSTONE-PROJECT
This repository contains the documentation for the Lita Capstone Project,focusing on sales analytics using Excel, SQL and PowerBI. The project aims to uncover key insights such as top-selling products, regional performance, and monthly sales trends. Additionally, The goal is to provide insight into average sales per product and total revenue by region, to inform business decisions. 

### PROJECT TITLE: SALES PERFORMANCE ANALYSIS

### PROJECT SCOPE:
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
```
Data Cleaning and Analysis on Excel: I removed duplicates by highligting and using the remove duplicates features, utilized Pivot tables to summarize data, Filter to improve data visualization and enhance insights, Charts to visualize trends and pattern, Slicer for interactive filtering.
Data Cleaning and Transformation on PowerBI: 
I used power query editor to clean and transform data.
i removed duplicates using remove Duplicates feature.
i changed data types using the data type feature.
I checked for data consistency using the column quality, column profile, and column distribution.
Data visualization: created interactive dashboards,used visualization(e.g, charts, cards,tables), filtered data using Slicers.
```
SQL

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

