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
