# LITA E-COMMERCE SALES ANALYSIS


## Table Of Content
 - [Project Overview](#project-overview)
 - [Data Sources](#data-sources)
 - [Data Collected](#data-collected)
 - [Tools Used](#tools-used)
 - [Data Cleaning /Preparation](#data-cleaning-/-preparation)
 - [Exploratory Data Analysis ](#exploratory-data-analysis)
 - [Data Analysis](#data-analysis)
 - [Results](#results)
 - [Findings](#findings)
 - [Recommendations](#recommendations)
 - [Limitations](#limitations)

###  Project Overview
This Project delves into the sales performance of a retail store,uncovering key trends and insights to inform business decisions.Through interactive visualizations and Data-Driven storytelling,we will explore:
- Top Selling products and categories.
- Regional Sales Performance and market trends.
- Monthly Sales fluctuations and seasonal patterns.

### Data Sources

Sales Data: The Primary Dataset used for this analysis is the "LITA Capstone Dataset.xlsx file contaiing detailed information about each sales from different customers.

### Data Collected 
The Dataset includes the following key columns:
1. Order ID: Unique identifier for each order.

2. Customer ID: Unique identifier for each customer.

3. Product:Name or description of the product sold. 

4. Region: Geographical area where sales Occured.

5. Order Date: Date when the order was placed.

6. Quantity: Number of units sold.

7. Unit Price:Price of a single unit of the product.

8. Total Sales: Total amount paid for the order.

### Tools Used
 -  Microsoft Excel [Download Here](https://wwww.microsoft.com)
    1. For Data Cleaning: Removing duplicates, data filtering,handling missing values were method used to clean the data to ensure the accuraccy and reliabilty of our analysis. 
    2. For Analysis:The data was analyzed, using Pivot table summarize and filter the data for each interpretation.

 - SQL Server - Data Analysis (Utilized for querying and manipulating large Datasets).

 - PowerBI -Creating Report (Employed For creating interactive dashboards and visualizations.

### Data Cleaning / Preparation
In the initial Data Preparation Phase,we performed the following tasks;
1. Data Loading and Inspection.

2. Handling Missing Values and Removing Duplicate.

3. Data Cleaning and Formatting.

### Exploratory Data Analysis 
   - What is the overall sales trend?
   - Which Products are top sellers?
   - What is the regional performance of each region?
   - What the Monthly sales trend ?

###  Data Analysis 
 Include some interesting code  worked with

 ```sql
select * from [dbo].[sales_data]


---TOTAL SALES FOR EACH PRODUCT CATEGORY--
Select Product, 
   sum(Total_Sales) As Total_Sales_by_Product from  [dbo].[sales_data]
   Group By Product
   Order by Total_Sales_by_Product DESC;

   ---NUMBER OF SALES TRANSACTION IN EACH REGION---
    Select Region,
    sum(Total_Sales) As Total_sales_by_Region from  [dbo].[sales_data]
    group by Region
    order by Total_sales_by_Region DESC;

	----HIGHEST SELLING PRODUCT BY TOTAL SALE VALUE==
    Select TOP 1 Product, 
    sum(Total_Sales) As Total_Sales from [dbo].[sales_data]
    Group By Product
    Order by Total_Sales DESC;
	
 ---TOTAL REVENUE PER PRODUCTS ---
  Select Product, Total_Sales
   from [dbo].[sales_data]

 ---  MONTHLY SALES TOTAL FOR THE CURRENT YEAR--
  Select Order_Month As Sales_Month,sum(Total_Sales) as  Total_Sales_by_month
   from [dbo].[sales_data]
   where Year(OrderDate) = '2024'
   group by Order_Month
   order by Total_Sales_by_month;

   ----Top 5 customer by total purchase amount-----
   Select * from [dbo].[sales_data]

   Select TOP 5 Customer_id,
   sum(Total_Sales) As Total_Sales_of_Top_5_customer 
	from [dbo].[sales_data]
    Group By Customer_Id
    Order by Total_Sales_of_Top_5_customer desc;

	----Percentage of total sale by contributed by each region----
	select Region, sum(Total_Sales) as Regional_sales,
	(sum(Total_Sales)*100/(select sum(Total_Sales) from [dbo].[sales_data] )) as percentage 
	from [dbo].[sales_data]
	group by Region
	order by Regional_sales desc;

	-------product with no sale in the last quater---
	select Product 
	from [dbo].[sales_data]
	where Product NOT IN 
	(Select DISTINCT Product from  [dbo].[sales_data]
	where OrderDate >= DATEADD(QUARTER,-1,GETDATE()))
	Group by Product
```

### Results

 The analysis results are summarised as follows:
 1. Sales Trend : Sales dropped by 10% YoY, with a significant drop in Q4.

 2. Product(Shoes)is the best performing category in term of sales .

 3. The South Region has the highest percentage of sales while other regions follows.

 4. The highest sales month was February with 25% of Total Sales .

### Findings 
1. Decline in Sales: Sales dropped across all regions and product categories.

2. Sales of product fluctuated significantly between 2023 and 2024 with no clear upward or downward trend.

3. Regional sales trends were unstable with south region experiencing a significant decline and west region showing growth.

4. Sales Peak in February and declined in March and preceeding month , indicating seasonal demang.

### Recommendations 
 Based on the analysis, i recommend the following :
1. Conduct market research to identify underlying causes of sales volatility, and enhanced seasonal marketing campaigns.

2. Develop Flexible pricing and inventory management strategies.

3. Tailor marketing strategies to regional market differences and invest in growing Regions.

### Limitations
   1. Data quality such as duplicate values were encountered.

   2. Sales data only represent specific Products.

   3. The analysis does not not account for external factors such as economic flunctuations.
  
