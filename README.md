# sales-analysis-dashboard
SQL Project to analyze sales data and generate insights


**Overview -**

This project is a **SQL-based Sales Analysis Dashboard** built using a realistic dataset of **Customers, Products, and Sales transactions**.  
The goal is to demonstrate **SQL skills in data modeling, querying, and generating business insights**.

 **Analysis Performed -**
- Total Revenue and Average Order Value  
- Top 5 Best-Selling Products  
- Revenue by Category and Region  
- Top Customers by Spending 
-  Most Frequent Customers  
- Daily Sale Summary
- Product Performance


**1. Total Sales Revenue -**

**SQL Code**
```sql
select sum(total_amount) as Total_Revenue from sales;
```
<img width="130" height="60" alt="Image" src="https://github.com/user-attachments/assets/31a15490-d0c4-4626-aa90-315e63db32e8" />


**2. Average Order Value -**

**SQL Code**
```sql
select avg(total_amount) as Avg_Order_value
from sales;
```

<img width="129" height="60" alt="Image" src="https://github.com/user-attachments/assets/113a5b4c-fa5c-43f1-9a3f-84e4d262ac60" />




**3. Top 5 Best-Selling Products -** 

**SQL Code**
```sql
 select p.name as Product,
 		sum(total_amount) as Total_sold
 from sales as s
 join products as p on p.product_id = s.product_id
 group by p.name
 order by total_sold desc
 limit 5; 

```

<img width="120" height="59" alt="Image" src="https://github.com/user-attachments/assets/0a8bc6d7-7cee-4c9c-9e87-b252523da18a" />


**4.  Revenue by Category -**

**SQL Code**
```sql
SELECT p.category, 
       SUM(s.total_amount) AS category_revenue
FROM Sales s
JOIN Products p ON s.product_id = p.product_id
GROUP BY p.category
ORDER BY category_revenue DESC;
```

<img width="198" height="110" alt="Image" src="https://github.com/user-attachments/assets/116e4fd2-f745-4d75-a572-4a3d9c3619c1" />


**5.  Revenue by Region -**

**SQL Code**
```sql
SELECT 
    c.region,
    SUM(s.total_amount) AS region_revenue
FROM Sales s
JOIN Customers c ON s.customer_id = c.customer_id
GROUP BY c.region
ORDER BY region_revenue DESC;
```

<img width="168" height="111" alt="Image" src="https://github.com/user-attachments/assets/6d0b2dc0-3af8-4337-838f-6ae83dc6a424" />


**6. Top 10 Customers by Spending -**

**SQL Code**
```sql
SELECT 
    c.name AS customer_name,
    SUM(s.total_amount) AS total_spent
FROM Sales s
JOIN Customers c ON s.customer_id = c.customer_id
GROUP BY c.name
ORDER BY total_spent DESC
LIMIT 10;
```

<img width="188" height="217" alt="Image" src="https://github.com/user-attachments/assets/66b47e4d-535d-4514-a039-937e3a3cd7e4" />


**7. Most Frequent Customers (by order count) -**

**SQL Code**
```sql
SELECT 
    c.name AS customer_name,
    COUNT(s.sale_id) AS total_orders
FROM Sales s
JOIN Customers c ON s.customer_id = c.customer_id
GROUP BY c.name
ORDER BY total_orders DESC
LIMIT 10;
```

<img width="201" height="223" alt="Image" src="https://github.com/user-attachments/assets/a7a4230f-176b-4927-82bb-56c6a3f2197d" />

**8. Daily Sales Summary -**






