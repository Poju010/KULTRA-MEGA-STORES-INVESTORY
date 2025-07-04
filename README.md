# KULTRA-MEGA-STORES-INVESTORY
## Project Overview
This project involves an in-depth SQL-based analysis of sales and inventory data for Kultra Mega Stores (KMS), a prominent retailer specializing in office supplies and furniture in Nigeria. As a Business Intelligence Analyst, this analysis aims to provide key insights and findings to the Business Manager of KMS's Abuja division, leveraging historical order data from 2009 to 2012.
## Dataset Description
This analysis utilizes two primary datasets:
- `KMS Sql Case Study.csv`: This is the main transactional dataset, containing historical sales and order data for Kultra Mega Stores from 2009 to 2012. Each row represents an order line item. Key columns include:
**Order and Sales Information:** Order ID, Order Date, Order Priority, Order Quantity, Sales, Discount, Profit, Unit Price, Shipping Cost, Ship Mode, Ship Date.
**Customer Demographics:** Customer Name, Customer Segment, Province, Region.
**Product Details:** Product Category, Product Sub-Category, Product Name, Product Container, Product Base Margin. 
- `Order_Status.csv:` This supplementary dataset provides information on the status of certain orders. It contains two key columns:
**Order ID:** To link with the main KMS Sql Case Study.csv data.
**Status:** Indicating the status of the order (e.g., 'Returned').  
These datasets collectively form the foundation for answering the various case scenarios and deriving actionable insights into KMS's sales performance, customer behavior, and operational efficiency.

## Goals and Objectives
The primary goal of this project is to leverage SQL to analyze Kultra Mega Stores' (KMS) sales and inventory data from 2009 to 2012, providing comprehensive insights to the Abuja division's Business Manager. This analysis aims to inform strategic decisions related to sales, customer management, and operational efficiency.
Specifically, this project will address the following key business questions, structured into two main case scenarios:

__Case Scenario I__: Sales Performance & Operational Efficiency
- Which product category had the highest sales?
- What are the Top 3 and Bottom 3 regions in terms of sales?
- What were the total sales of appliances in Ontario?
- Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers.
- KMS incurred the most shipping cost using which shipping method?

__Case Scenario II__: Customer Behavior & Profitability
- Who are the most valuable customers, and what products or services do they typically purchase?
- Which small business customer had the highest sales?
- Which Corporate Customer placed the most number of orders in 2009 – 2012?
- Which consumer customer was the most profitable one?
- Which customer returned items, and what segment do they belong to?
- If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer.
  
By answering these questions, the project aims to provide actionable recommendations for improving sales strategies, optimizing shipping logistics, and enhancing customer relationships for KMS.

## Analysis and Key Findings  
**Case Scenario I**
```
---(Q1) Which product category had the highest sales?
SELECT TOP 1 
    product_category, 
    SUM(Sales) AS [Total Sales]
FROM 
    [sales-data]
GROUP BY 
    product_category
ORDER BY 
    [Total Sales] DESC;
```

```
---(Q2) What are Top 3 and Bottom 3 regions in terms of sales?
---TOP 3
SELECT Top 3 
    Region,    
    sum(sales) as [Total Sales]
FROM 
    [sales-data]
GROUP BY 
    Region
ORDER BY 
    [Total Sales] DESC

---BOTTOM 3
SELECT TOP 3 
    Region, 
    sum(sales) as [Total Sales]
FROM 
    [sales-data]
GROUP BY 
    Region
ORDER BY 
    [Total Sales] ASC;
```

```
---(Q3) What were the total sales of appliances in Ontario?
SELECT  
    Province, 
    Product_Sub_Category, 
    sum(sales) as [Total Sales]
FROM 
    [sales-data]
WHERE 
    Province = 'Ontario' AND Product_Sub_Category = 'appliances'
GROUP BY 
    Province, 
    Product_Sub_Category;
```

```
---(Q4) Advise the management of KMS on what to do to increase the revenue from the bottom 10 customer
SELECT TOP 10 
    Customer_Name, 
    sum(sales) AS [Total Sales]
FROM 
    [sales-data]
GROUP BY 
    Customer_Name
ORDER BY 
    [Total Sales] ASC;
```

```
---(Q5) KMS incurred the most shipping cost using which shipping method?
SELECT 
    Ship_Mode, 
    sum(Shipping_Cost) AS Total_Shipping_Cost
FROM 
    [sales-data]
GROUP BY 
    Ship_Mode
ORDER BY 
    Total_Shipping_Cost DESC;
```

**Case Scenario II**
```
---(Q6) Who are the most valuable customers, and what products or services do they typically purchase? 
---(Q6a)
SELECT top 10 
    Customer_Name, 
    Customer_Segment, 
    Product_Category, 
    Product_Sub_Category,
    sum(profit) AS TotalProfit, 
    sum(sales) AS TotalSales 
FROM 
    [sales-data]
GROUP BY 
    Customer_Name, Customer_Segment, Product_Category, Product_Sub_Category
ORDER BY 
    TotalProfit DESC;
---(Q6b)
SELECT
    sd.Customer_Name,
    sd.Product_Category,
    sd.Product_Sub_Category,
    COUNT(sd.Product_Name) AS NumberOfPurchases,
    SUM(sd.Sales) AS TotalSalesOfProduct
FROM
    [sales-data] sd
WHERE
    sd.Customer_Name IN ('Emily Phan', 'Grant Carroll', 'Raymond Book', 'Clytie Kelty', 'Andy Reiter',
                         'Deborah Brumfield', 'Karen Carlisle', 'Rick Wilson', 'Logan Haushalter', 'Nick Crebassa') 
GROUP BY
    sd.Customer_Name,
    sd.Product_Category,
    sd.Product_Sub_Category
ORDER BY
    sd.Customer_Name, NumberOfPurchases DESC;
```

```
--- (Q7) Which small business customer had the highest sales? 
SELECT top 1
    Customer_Name,
    customer_segment,
    sum(sales) as TotalSales
FROM
    [sales-data]
WHERE
    customer_segment = 'small business'
GROUP BY
    Customer_Name,
    customer_segment
ORDER BY
    TotalSales DESC;
```

```
--- (Q8) Which Corporate Customer placed the most number of orders in 2009 – 2012? 
SELECT TOP 1
    [Customer_Name],
    [Customer_Segment], 
    COUNT(Order_ID) AS [Number Of Orders]
FROM 
    [sales-data]
WHERE 
    Customer_Segment = 'Corporate' AND year(Order_Date) between 2009 and 2012 
GROUP BY
    [Customer_Name],[Customer_Segment]
ORDER BY 
    [Number Of Orders] DESC;
```

```
--- (Q9) Which consumer customer was the most profitable one?
SELECT TOP 1 
    Customer_Name, 
    Customer_Segment, 
    SUM(PROFIT) AS TotalProfit
FROM 
    [sales-data]
WHERE 
    Customer_Segment = 'Consumer'
GROUP BY 
    Customer_Name, Customer_Segment
ORDER BY 
    TotalProfit DESC;
```

```
--- (Q10) Which customer returned items, and what segment do they belong to? 
SELECT 
    sd.Customer_Name, 
    sd.Customer_Segment,
    os.[Status]
FROM 
    [sales-data] sd
JOIN 
    Order_Status os ON os.Order_ID = sd.Order_ID
WHERE
    os.[Status] = 'Returned';
```

```
--- (Q11) If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer 
SELECT 
    Ship_Mode,
    Order_Priority,
    count(order_id) as [Number Of Orders],
    sum(order_quantity) as TotalOrderQuantity,
    sum(shipping_cost) as TotalShippingCost,
    avg(shipping_cost) as AverageShippingCost
FROM 
    [sales-data]
GROUP BY
    Ship_Mode,
    Order_Priority
ORDER BY 
    Ship_Mode,
    Order_Priority;
```

