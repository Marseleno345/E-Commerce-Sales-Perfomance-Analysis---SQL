# Brazilian E-Commerce-Sales-Perfomance-Analysis-SQL
Analyzing sales data using SQL to identify top-performing products, customers, categories, revenue drivers, and sales trends with focus on turing raw data into meaningful business insights 
This project explores a fictional sales database to analyze product performance, customer behavior and other businesses question to answer using SQL.

# Database Schema
Below is the Schema used for the analysis:
<img width="3000" height="2325" alt="inbox_2473556_23a7d4d8cd99e36e32e57303eb804fff_db-schema" src="https://github.com/user-attachments/assets/e614d576-1230-4396-90b9-6e3892a2fbfd" />
----
# Question 1: Which products are ordered most frequently?

  ## SQL Query:
  ```Sql query
SELECT pcnt.product_category_name_english,COUNT(oi.order_item_id ) AS 'total_count' 
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name 
JOIN order_items oi
USING (product_id)
GROUP BY p.product_category_name 
ORDER BY COUNT(product_id) DESC
LIMIT 20
```
## The result of the top 20 shows:

- Most categories have a category name.

- showing that the most ordered products of 11,115 are bed_bath_table.

<img width="416" height="536" alt="Capture2" src="https://github.com/user-attachments/assets/49b09af4-f91e-4cb4-a5a4-3817b34bbc7f" />

## Question 2: Which products generate the most revenues?

## SQL Query:
```sql
SELECT pcnt.product_category_name_english,SUM(op.payment_value ) AS 'Revenue'
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name
JOIN order_items oi 
USING(product_id)
JOIN order_payments op
ON oi.order_id = op.order_id
GROUP BY pcnt.product_category_name_english
ORDER BY SUM(op.payment_value) DESC
LIMIT 20
```
## The results of top 20 shows:

- that the most products that generate revenues are bed_bath_table and also validates that these products are the most ordered.

<img width="407" height="552" alt="Capture3" src="https://github.com/user-attachments/assets/1510c521-926a-42d6-9726-62cff7b82c91" />
