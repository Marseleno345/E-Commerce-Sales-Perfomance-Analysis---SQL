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

# Question 2: Which products generate the most revenues?

## SQL Query:
```sql
SELECT pcnt.product_category_name_english,SUM(oi.price) AS 'Revenue'
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name
JOIN order_items oi 
USING(product_id)
GROUP BY pcnt.product_category_name_english
ORDER BY Revenue DESC
LIMIT 20

```
## The results of top 20 shows:

- that the most products that generate revenues are Health_beauty being the first.
- while second are watches_gifts.
- and third bed_bath_table.

<img width="406" height="546" alt="Capture3" src="https://github.com/user-attachments/assets/62a41101-4d25-47c5-8f4c-74781185aca8" />

### ***Which does raise another important question***.

# How does health_beauty generate more revenue while having lower order Counts than Bed_bath_table?

## SQL Query:
``` sql
SELECT pcnt.product_category_name_english,AVG(oi.price) AS 'Avg_prices'
FROM products p 
JOIN product_category_name_translation pcnt 
ON pcnt.product_category_name = p.product_category_name
JOIN order_items oi 
USING(product_id)
WHERE pcnt.product_category_name_english IN('health_beauty','bed_bath_table','watches_gifts')
GROUP BY pcnt.product_category_name_english 
ORDER BY Avg_prices  DESC 
```
- the query results does show that the average prices for the top 3 product_category.
- which does show that watches_gifts does have the highest average prices and since it does have lower order counts than both categories then it does generate lower revenue caused by it's high average prices.
- but as for health_beauty it shows that it does have higher average price than bed_bath_table.

<img width="413" height="84" alt="Capture4" src="https://github.com/user-attachments/assets/05ce19c9-56da-47c7-a318-02fe33779597" />

