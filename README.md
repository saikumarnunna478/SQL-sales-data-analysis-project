# SQL-sales-data-analysis-project
## 📊 Project Overview
This project focuses on analyzing retail sales data using SQL:
## 🎯 Business Questions Answered
1. What are the top 5 most selling products by quantity?
2. Which products are most frequently cancelled?
3. What times of the day has the highest number of purchases?
4. Who are the top 5 highest spending customers?
5. Which product categories generate the highest revenue?
6. What is the return/cancellation rate per product category?
7. What is the preferred payment mode?
8. How does age group affect purchasing behaviour?
9. What is the monthly sales trend?
10. Are certain genders buying more specific product categories?
11. How many orders are pending?
12. Revenue from furniture(delivered)?

## 🛠️ Tech Stack & Tools
* **Database System:** [MySQL]
* **Language:** SQL (DQL, Aggregations, Joins, Subqueries, CTEs)
## 🗂️ Database Schema & Dataset

The analysis is based on a relational database containing the following core tables:
* **`orders`**: Contains transaction IDs, customer IDs, order dates, sale amounts, and delivery status.
* **`products`**: Contains product IDs, names, categories, and unit prices.

> *Note: The raw dataset used for this project can be found in the `/data` folder of this repository.*

## 🔍 Key SQL Queries & Insights

### 1.Top 5 most selling products by quantity (Delivered Only)
* **Query:**
 ``` sql
SELECT
  select 
	 	 	 product_name,
  Sum(quantiy) As Total_Quantity
                		from sales
  where status = 'Delivered'
  group by Product_name
  order by Total_Quantity Desc
  Limit 5;

