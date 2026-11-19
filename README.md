# Olist E-Commerce Sales & Category Analysis:
A Power BI dashboard built on the Brazilian E-Commerce Public Dataset by Olist. The data lives in a SQLite database, was explored and queried with SQL in DBeaver, and was visualised in Power BI through an ODBC connection.

# Dashboard:
<img width="1320" height="746" alt="Screenshot (554)" src="https://github.com/user-attachments/assets/59d8d812-5dc5-43d1-865a-d11fd604565f" />

# Questions answered:

1- Which product categories are ordered the most?

2- Which categories generate the most revenue?

Tools Used:
- SQLite: the database
- DBeaver: writing and testing the SQL
- Power BI Desktop: dashboard (connected via the SQLite ODBC driver)

# Database Schema

Below is the Schema used for the analysis:

<img width="3000" height="2325" alt="inbox_2473556_23a7d4d8cd99e36e32e57303eb804fff_db-schema" src="https://github.com/user-attachments/assets/e614d576-1230-4396-90b9-6e3892a2fbfd" />
----

# Question 1: Which product categories are ordered the most?

  ## SQL Query:
  ```Sql query
SELECT pcnt.product_category_name_english,COUNT(DISTINCT o.order_id ) AS 'total_count',
1.0*COUNT(DISTINCT o.order_id )/(SELECT COUNT(*) FROM orders o2 WHERE o2.order_status NOT IN ('canceled','unavaliable') ) AS 'Percentage of Total'
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name 
JOIN order_items oi
USING (product_id)
JOIN orders o 
USING (order_id)
WHERE o.order_status NOT IN ('canceled','unavailable')
GROUP BY p.product_category_name 
ORDER BY total_count DESC
LIMIT 20
```
## The result of the top 20 shows:

- showing that the most ordered products of 9,399 are bed_bath_table.

- The percentage of each category over the total orders.

- Canceled and unavailable orders are excluded. 

<img width="845" height="786" alt="Screenshot (555)" src="https://github.com/user-attachments/assets/f018623d-25c6-4b9b-b47f-1c122bfee572" />

# Question 2: Which categories generate the most revenue?

## SQL Query:
```sql
SELECT pcnt.product_category_name_english,SUM(oi.price) AS 'Revenue'
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name
JOIN order_items oi 
USING(product_id)
JOIN orders o 
USING (order_id)
WHERE o.order_status NOT IN ('canceled','unavailable')
GROUP BY pcnt.product_category_name_english
ORDER BY Revenue DESC
LIMIT 20
```
## The results of top 20 shows:

- that the most products that generate revenues are Health_beauty being the first.
- while second are watches_gifts.
- and third bed_bath_table.

<img width="848" height="995" alt="Screenshot (556)" src="https://github.com/user-attachments/assets/be5e4891-5964-455b-8927-b7dc7923dd3f" />


### ***Which does raise another important question???***.

# Question 3: Does the most ordered products are the same products that generate the most revenue?

to answer this question we need to get the average price for the top 20 products category. 

## SQL Query:
``` sql
SELECT pcnt.product_category_name_english,ROUND(AVG(oi.price),0) AS 'Avg_prices'
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name
JOIN order_items oi 
USING(product_id)
JOIN orders o 
USING (order_id)
WHERE o.order_status NOT IN ('canceled','unavailable')
GROUP BY pcnt.product_category_name_english 
ORDER BY Avg_prices DESC
LIMIT 20
```
- the query results does show that the average prices for the top 20 product category.
- it shows that watches_gifts is one of the top 20. 

<img width="848" height="970" alt="Screenshot (558)" src="https://github.com/user-attachments/assets/f881d7dd-6bad-4aab-8019-2524e4c90a83" />






