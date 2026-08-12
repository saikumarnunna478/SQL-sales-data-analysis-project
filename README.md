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
* **Business Need:**Identify the top 5 fastest-moving products based on total units sold.
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
  Limit 5;```

###2.Which product’s are most frequently cancelled?
* **Business Need:**Identify which items are most frequently cancelled by customers.
* **Query:**
```Sql
SELECT
	product_name,
    Count(Status) As Cancelled_products
From sales
where Status = 'Cancelled'
group by product_name 
order by Cancelled_products Desc
limit 10;```

###3.What time’s of the day has the highest number of purchases?
* **Business Need:**Determine the specific hours of the day when customers place the highest volume of orders.
* **Query:**
```Sql
SELECT
	case 
		when hour (time_of_purchase) between 6 and 11 then 'Morning'
 		when hour (time_of_purchase) between 12 and 17 then 'Afternoon'
 		when hour (time_of_purchase) between 18 and 23 then 'Evening'
 		Else 'Night'
 		End as time_of_day,
		count(*) as Total_order
	from sales
 	group by time_of_day
 	order by Total_order Desc;```

###4.Who are the top 5 highest spending customers?
* **Business Need:**Identify the top 5 customers who have generated the most revenue for the business.
* **Query:**
```Sql
SELECT
	customer_id,
 	customer_name,
	Sum(quantiy * prce ) as Total_spending_by_customer
from sales
where status = 'Delivered'
group by customer_id,Customer_name
order by Total_spending_by_customer Desc
limit 5;```




##

