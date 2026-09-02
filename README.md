# Brazilian E-Commerce-Sales-Perfomance-Analysis---SQL
Analyzing sales data using SQL to identify top-performing products, customers, categories, revenue drivers, and sales trends with focus on turing raw data into meaningful business insights 
This project explores a fictional sales database to analyze product performance, customer behavior and other businesses question to answer using SQL.

# Database Schema
Below is the Schema used for the analysis:
<img width="3000" height="2325" alt="inbox_2473556_23a7d4d8cd99e36e32e57303eb804fff_db-schema" src="https://github.com/user-attachments/assets/e614d576-1230-4396-90b9-6e3892a2fbfd" />
----
# Question 1: Which products are ordered most frequently?

  ## SQL Query
  ```Sql query
SELECT p.product_category_name ,COUNT(oi.order_item_id ) AS 'total_count' 
FROM products p 
LEFT JOIN order_items oi 
USING (product_id)
GROUP BY p.product_category_name 
ORDER BY COUNT(product_id) DESC 
```
## Your result shows:

- Most categories have a category name.

- 1,603 records have NULL for product_category_name.

- showing that the most ordered products is cama_mesa_banho which means bed,tables and bath.

<img width="378" height="631" alt="Capture2" src="https://github.com/user-attachments/assets/a7115075-0826-4004-ba52-379908780f13" />
