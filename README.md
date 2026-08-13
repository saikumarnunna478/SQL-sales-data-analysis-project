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
9. Are certain genders buying more specific product categories?
10. How many orders are pending?
11. Revenue from furniture(delivered)?

## 🛠️ Tech Stack & Tools
* **Database System:** [MySQL]
* **Language:** SQL (DQL, Aggregations, Joins, Subqueries, CTEs)
## 🗂️ Database Schema & Dataset

The analysis is based on a relational database containing the following core tables:
* **`orders`**: Contains transaction IDs, customer IDs, order dates, sale amounts, and delivery status.
* **`products`**: Contains product IDs, names, categories, and unit prices.

> *Note: The raw dataset used for this project can be found in the `/data` folder of this repository.*

## 🔍 Key SQL Queries & Insights

###1.Top 5 most selling products by quantity (Delivered Only)?
* **Business Need:**Identify the top 5 fastest-moving products based on total units sold.
* **Query:**
 ```Sql
	SELECT
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

###5.Which Product categories generate the highest revenue?
* **Business Need:**Rank product categories based on total sales revenue to identify primary business drivers.
* **Query:**
```Sql
	SELECT
		product_category,
 		sum(quantiy * prce) as Highest_Revenue
	from sales
	where status = 'delivered'
	group by product_category 
	order by Highest_Revenue Desc
	Limit 10;```

###6.What is the return/cancellation rate per product category?
* **Business Need:**Calculate the percentage of orders that get cancelled or returned for every product category.
* **Query:**
```Sql
	SELECT
		product_category,
 		count(*) as Total_order,
 		sum(status = 'Returned') as Returned_orders,
		sum(status = 'Cancelled') as cancelled_orders,
 		round(sum(status = 'Returned')/count(*),2) As Return_rate,
 		round(sum(status = 'Cancelled')/count(*),2)as Cancelled_rate
	from sales
	group by product_category;```

###7.What is the preferred payment mode?
* **Business Need:**Identify which payment methods (e.g., Credit Card, UPI, Debit Card, EMI, or Cash) customers use most frequently.
* **Query:**
```Sql
	SELECT
		payment_mode,
    	count(*) as Total_count
	from Sales
	group by payment_mode
	order by Total_count Desc;```

###8.How does age group effect purchasing behaviour?
* **Business Need:**Understand how customer age impacts average spending, total order volume, and category preferences.
* **Query:**
```Sql
	SELECT
		case
			when Customer_age Between 18 and 25 then '18-25'
        	when customer_age Between 26 and 35 then '26-35'
 	 		when customer_age Between 36 and 50 then '36-50'
        	else '51+'
 			end  as age_group,
			sum(quantity*price) as Total_Purchase_by_age
	From sales 
	group by age_group
	order by Total_purchase_by_age;'''
		
###9.Are Certain genders buying more specific product categories?
* **Business Need:**Cross-analyze customer gender against product categories to discover demographic purchasing trends.
* **Query:**
```Sql
	SELECT
		Product_category,
 		gender,
    	count(*) as Total_count
	from sales
	group by Product_category,gender
	order by Total_count;'''
		
###10.How many orders are pending?
* **Business Need:**Determine the exact number of orders currently stuck in a "Pending" status and their total financial value.
* **Query:**
```Sql
	SELECT
		status,
    	count(*) as Total_Pending
	from sales
	where status = 'Delivered'
	group by status;'''

###11.Revenue from furniture(delivered)?
* **Business Need:**Calculate the exact realized revenue from the furniture segment by filtering out fulfilled orders.
* **Query:**
```Sql
	SELECT
		Product_category,
    	Sum(quantity*price) As Total_revenue
	from sales 
	where product_category = 'Furniture' and status = 'Delivered'
	group by product_category;'''

## 📂 How to Run the Project
1. Clone this repository to your local machine.
2. Import the provided dataset file (`.csv`) into your SQL database.
3. Run the `sales_analysis.sql` script to generate the tables and views.
		

		

``

##
