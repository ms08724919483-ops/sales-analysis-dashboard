# Sales Analysis Dashboard
SQL Project to analyze sales data and generate insights.


## 📊 Project Overview

This project is a **SQL-based Sales Analysis Dashboard** built using a realistic dataset of **Customers, Products, and Sales transactions**.  
The goal is to demonstrate **SQL skills in data modeling, querying, and generating business insights**.

&ensp;

## 🗄️ Database Schema
The database has **3 core tables**:

- **customers** → customers info  
- **products** → product catalog with category & price  
- **sales** → sales transactions 

&ensp;

## 🔍 Example Analysis Queries
- Total Revenue and Average Order Value  
- Top 5 Best-Selling Products  
- Revenue by Category and Region  
- Top Customers by Spending 
-  Most Frequent Customers  
- Daily Sale Summary
- Product Performance

&ensp;

**1. <ins>Total Sales Revenue -</ins>**



**SQL Code**
```sql
select sum(total_amount) as Total_Revenue from sales;
```
<img width="130" height="60" alt="Image" src="https://github.com/user-attachments/assets/31a15490-d0c4-4626-aa90-315e63db32e8" />

&ensp;

**2. <ins>Average Order Value -</ins>**

**SQL Code**
```sql
select avg(total_amount) as Avg_Order_value
from sales;
```

<img width="129" height="60" alt="Image" src="https://github.com/user-attachments/assets/113a5b4c-fa5c-43f1-9a3f-84e4d262ac60" />

&ensp;


**3. <ins>Top 5 Best-Selling Products -</ins>** 

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

<img width="169" height="127" alt="image" src="https://github.com/user-attachments/assets/fc42645a-a157-4407-b1f1-c65035e1f14d" />



&ensp;

**4. <ins>Revenue by Category -</ins>**

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

&ensp;

**5. <ins>Revenue by Region -</ins>**

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

&ensp;

**6. <ins>Top 10 Customers by Spending -</ins>**

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

&ensp;

**7. <ins>Most Frequent Customers (by order count) -</ins>**

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

&ensp;

**8. <ins>Daily Sales Summary -</ins>**

**SQL Code**
```sql

SELECT 
    date,
    SUM(total_amount) AS daily_revenue,
    COUNT(sale_id) AS total_orders
FROM Sales
GROUP BY date
ORDER BY date;
```


| date       | daily_revenue | total_orders |
|------------|---------------|--------------|
| 01-01-2024 | 8176          | 1            |
| 02-01-2024 | 6120          | 2            |
| 04-01-2024 | 4822          | 1            |
| 08-01-2024 | 2147          | 1            |
| 09-01-2024 | 9625          | 3            |
| 10-01-2024 | 6220          | 2            |
| 14-01-2024 | 8962          | 1            |
| 15-01-2024 | 8164          | 2            |
| 17-01-2024 | 19056         | 2            |
| 19-01-2024 | 25960         | 3            |
| 20-01-2024 | 10090         | 3            |
| 21-01-2024 | 13099         | 2            |
| 23-01-2024 | 8962          | 1            |
| 25-01-2024 | 6441          | 1            |
| 26-01-2024 | 13156         | 2            |
| 27-01-2024 | 15932         | 2            |
| 28-01-2024 | 4863          | 1            |
| 31-01-2024 | 14466         | 1            |
| 01-02-2024 | 14020         | 2            |
| 03-02-2024 | 8176          | 1            |
| 04-02-2024 | 7670          | 2            |
| 06-02-2024 | 4481          | 1            |
| 07-02-2024 | 21970         | 3            |
| 09-02-2024 | 41788         | 5            |
| 11-02-2024 | 6580          | 3            |
| 13-02-2024 | 10677         | 1            |
| 16-02-2024 | 22827         | 3            |
| 18-02-2024 | 9834          | 1            |
| 19-02-2024 | 19579         | 4            |
| 20-02-2024 | 13179         | 1            |
| 22-02-2024 | 20074         | 2            |
| 25-02-2024 | 8176          | 1            |
| 26-02-2024 | 9478          | 1            |
| 27-02-2024 | 4590          | 1            |
| 28-02-2024 | 26889         | 5            |
| 29-02-2024 | 8741          | 2            |
| 01-03-2024 | 6441          | 1            |
| 02-03-2024 | 19672         | 3            |
| 03-03-2024 | 2132          | 1            |
| 05-03-2024 | 24591         | 3            |
| 08-03-2024 | 9644          | 1            |
| 11-03-2024 | 14986         | 2            |
| 12-03-2024 | 3768          | 1            |
| 13-03-2024 | 15667         | 2            |
| 14-03-2024 | 6730          | 3            |
| 15-03-2024 | 4393          | 1            |
| 16-03-2024 | 1530          | 1            |
| 17-03-2024 | 1530          | 1            |
| 19-03-2024 | 8421          | 2            |
| 20-03-2024 | 9726          | 1            |
| 21-03-2024 | 8492          | 2            |
| 22-03-2024 | 17262         | 2            |
| 24-03-2024 | 2147          | 1            |
| 25-03-2024 | 6992          | 2            |
| 28-03-2024 | 9159          | 1            |
| 29-03-2024 | 8609          | 2            |
| 30-03-2024 | 20155         | 2            |
| 01-04-2024 | 7932          | 1            |
| 02-04-2024 | 32969         | 5            |
| 03-04-2024 | 8540          | 2            |
| 04-04-2024 | 13179         | 1            |
| 05-04-2024 | 7118          | 1            |
| 06-04-2024 | 5556          | 1            |
| 07-04-2024 | 10844         | 3            |
| 08-04-2024 | 1530          | 1            |
| 09-04-2024 | 9478          | 1            |
| 11-04-2024 | 15418         | 2            |
| 12-04-2024 | 7258          | 2            |
| 16-04-2024 | 4393          | 1            |
| 17-04-2024 | 5556          | 1            |
| 18-04-2024 | 4834          | 2            |
| 19-04-2024 | 6965          | 2            |
| 20-04-2024 | 3053          | 1            |
| 21-04-2024 | 14217         | 1            |
| 22-04-2024 | 7902          | 2            |
| 23-04-2024 | 16641         | 2            |
| 24-04-2024 | 8786          | 1            |
| 25-04-2024 | 15317         | 2            |
| 27-04-2024 | 1852          | 1            |
| 28-04-2024 | 14128         | 2            |
| 30-04-2024 | 4822          | 1            |
| 01-05-2024 | 4294          | 1            |
| 02-05-2024 | 15392         | 2            |
| 03-05-2024 | 19328         | 2            |
| 04-05-2024 | 10679         | 2            |
| 05-05-2024 | 4198          | 1            |
| 07-05-2024 | 16232         | 2            |
| 08-05-2024 | 10478         | 3            |
| 09-05-2024 | 4198          | 1            |
| 10-05-2024 | 2402          | 1            |
| 11-05-2024 | 4590          | 1            |
| 12-05-2024 | 5556          | 1            |
| 14-05-2024 | 9159          | 1            |
| 15-05-2024 | 38549         | 4            |
| 16-05-2024 | 3060          | 1            |
| 19-05-2024 | 21438         | 3            |
| 20-05-2024 | 13443         | 1            |
| 21-05-2024 | 15015         | 3            |
| 22-05-2024 | 6715          | 2            |
| 24-05-2024 | 7347          | 2            |
| 25-05-2024 | 19797         | 3            |
| 26-05-2024 | 10209         | 2            |
| 27-05-2024 | 8910          | 2            |
| 29-05-2024 | 9932          | 2            |
| 31-05-2024 | 21712         | 5            |
| 01-06-2024 | 24051         | 2            |
| 02-06-2024 | 24009         | 3            |
| 03-06-2024 | 8286          | 2            |
| 06-06-2024 | 8962          | 1            |
| 07-06-2024 | 14751         | 1            |
| 08-06-2024 | 26471         | 3            |
| 09-06-2024 | 14589         | 1            |
| 10-06-2024 | 3053          | 1            |
| 11-06-2024 | 11304         | 1            |
| 12-06-2024 | 3966          | 1            |
| 13-06-2024 | 6393          | 2            |
| 14-06-2024 | 16883         | 2            |
| 15-06-2024 | 9644          | 1            |
| 16-06-2024 | 8508          | 2            |
| 17-06-2024 | 14258         | 3            |
| 18-06-2024 | 9159          | 2            |
| 19-06-2024 | 23179         | 2            |
| 21-06-2024 | 24585         | 2            |
| 22-06-2024 | 18183         | 2            |
| 23-06-2024 | 21556         | 2            |
| 24-06-2024 | 8013          | 1            |
| 27-06-2024 | 3704          | 1            |
| 28-06-2024 | 11867         | 3            |
| 29-06-2024 | 27396         | 2            |
| 30-06-2024 | 6441          | 1            |
| 02-07-2024 | 19312         | 2            |
| 03-07-2024 | 10677         | 1            |
| 04-07-2024 | 27080         | 4            |
| 06-07-2024 | 31566         | 3            |
| 07-07-2024 | 22764         | 2            |
| 10-07-2024 | 1530          | 1            |
| 13-07-2024 | 8508          | 2            |
| 14-07-2024 | 12000         | 3            |
| 15-07-2024 | 11600         | 3            |
| 17-07-2024 | 14718         | 2            |
| 18-07-2024 | 13443         | 1            |
| 22-07-2024 | 8962          | 1            |
| 24-07-2024 | 9726          | 1            |
| 25-07-2024 | 14643         | 2            |
| 26-07-2024 | 6106          | 2            |
| 27-07-2024 | 4088          | 1            |
| 28-07-2024 | 16281         | 2            |
| 30-07-2024 | 19285         | 2            |
| 31-07-2024 | 14119         | 2            |
| 01-08-2024 | 3198          | 1            |
| 02-08-2024 | 14217         | 1            |
| 03-08-2024 | 26609         | 3            |
| 04-08-2024 | 9159          | 1            |
| 05-08-2024 | 11094         | 2            |
| 06-08-2024 | 11448         | 2            |
| 07-08-2024 | 2235          | 1            |
| 08-08-2024 | 14958         | 2            |
| 10-08-2024 | 12413         | 2            |
| 11-08-2024 | 15648         | 3            |
| 12-08-2024 | 18739         | 3            |
| 13-08-2024 | 13444         | 2            |
| 14-08-2024 | 29847         | 5            |
| 15-08-2024 | 2235          | 1            |
| 16-08-2024 | 6705          | 1            |
| 17-08-2024 | 8852          | 2            |
| 18-08-2024 | 16689         | 3            |
| 20-08-2024 | 20678         | 3            |
| 21-08-2024 | 4739          | 1            |
| 22-08-2024 | 4822          | 1            |
| 23-08-2024 | 4822          | 1            |
| 24-08-2024 | 9644          | 1            |
| 25-08-2024 | 36447         | 3            |
| 27-08-2024 | 15996         | 2            |
| 28-08-2024 | 25836         | 3            |
| 30-08-2024 | 22489         | 3            |
| 01-09-2024 | 2132          | 1            |
| 03-09-2024 | 4917          | 1            |
| 04-09-2024 | 29819         | 3            |
| 05-09-2024 | 4088          | 1            |
| 06-09-2024 | 13256         | 2            |
| 07-09-2024 | 13640         | 2            |
| 08-09-2024 | 17820         | 2            |
| 09-09-2024 | 3198          | 1            |
| 11-09-2024 | 13092         | 2            |
| 12-09-2024 | 4088          | 1            |
| 14-09-2024 | 5851          | 2            |
| 15-09-2024 | 10323         | 2            |
| 16-09-2024 | 10456         | 3            |
| 17-09-2024 | 4863          | 1            |
| 18-09-2024 | 4470          | 1            |
| 19-09-2024 | 6021          | 2            |
| 20-09-2024 | 8013          | 1            |
| 22-09-2024 | 16641         | 2            |
| 24-09-2024 | 10684         | 2            |
| 25-09-2024 | 9834          | 1            |
| 26-09-2024 | 8425          | 2            |
| 27-09-2024 | 8176          | 1            |
| 28-09-2024 | 37494         | 3            |
| 29-09-2024 | 5556          | 1            |
| 30-09-2024 | 24395         | 2            |
| 02-10-2024 | 28586         | 3            |
| 03-10-2024 | 15787         | 3            |
| 04-10-2024 | 3966          | 1            |
| 05-10-2024 | 6106          | 1            |
| 06-10-2024 | 4653          | 1            |
| 08-10-2024 | 6705          | 1            |
| 09-10-2024 | 4917          | 1            |
| 10-10-2024 | 8029          | 2            |
| 11-10-2024 | 14217         | 1            |
| 13-10-2024 | 6201          | 2            |
| 14-10-2024 | 15068         | 2            |
| 15-10-2024 | 5465          | 3            |
| 16-10-2024 | 28263         | 4            |
| 18-10-2024 | 3053          | 1            |
| 19-10-2024 | 12554         | 2            |
| 21-10-2024 | 9478          | 1            |
| 22-10-2024 | 2671          | 1            |
| 23-10-2024 | 14217         | 1            |
| 24-10-2024 | 8962          | 1            |
| 26-10-2024 | 11535         | 2            |
| 28-10-2024 | 23252         | 2            |
| 29-10-2024 | 6705          | 1            |
| 30-10-2024 | 9159          | 1            |
| 31-10-2024 | 25323         | 4            |
| 01-11-2024 | 26074         | 5            |
| 02-11-2024 | 1530          | 1            |
| 04-11-2024 | 1066          | 1            |
| 05-11-2024 | 3559          | 1            |
| 06-11-2024 | 22521         | 3            |
| 07-11-2024 | 4818          | 2            |
| 08-11-2024 | 29951         | 4            |
| 10-11-2024 | 9644          | 2            |
| 11-11-2024 | 3737          | 2            |
| 13-11-2024 | 26022         | 3            |
| 14-11-2024 | 1066          | 1            |
| 16-11-2024 | 16646         | 2            |
| 17-11-2024 | 23748         | 2            |
| 19-11-2024 | 9561          | 2            |
| 20-11-2024 | 6637          | 2            |
| 21-11-2024 | 11898         | 1            |
| 25-11-2024 | 12022         | 2            |
| 26-11-2024 | 14399         | 3            |
| 27-11-2024 | 13436         | 2            |
| 29-11-2024 | 1201          | 1            |
| 01-12-2024 | 2671          | 1            |
| 03-12-2024 | 12315         | 2            |
| 04-12-2024 | 17032         | 3            |
| 05-12-2024 | 15816         | 4            |
| 08-12-2024 | 7670          | 2            |
| 09-12-2024 | 13393         | 2            |
| 10-12-2024 | 4739          | 1            |
| 11-12-2024 | 23683         | 4            |
| 12-12-2024 | 18455         | 2            |
| 13-12-2024 | 17409         | 2            |
| 15-12-2024 | 6705          | 1            |
| 17-12-2024 | 21807         | 3            |
| 18-12-2024 | 7536          | 1            |
| 19-12-2024 | 16322         | 2            |
| 20-12-2024 | 2132          | 1            |
| 21-12-2024 | 1201          | 1            |
| 22-12-2024 | 33777         | 4            |
| 23-12-2024 | 4917          | 1            |
| 24-12-2024 | 2235          | 1            |
| 25-12-2024 | 12264         | 1            |
| 26-12-2024 | 28826         | 3            |
| 27-12-2024 | 4088          | 1            |
| 28-12-2024 | 3603          | 1            |
| 29-12-2024 | 18760         | 2            |
| 30-12-2024 | 1066          | 1            |
| 31-12-2024 | 10677         | 1            |

&ensp;

**9. <ins>Product Performance (revenue + units sold) -</ins>**

**SQL Code**
```sql

SELECT 
    p.name AS product_name,
    p.category,
    SUM(s.quantity) AS total_units_sold,
    SUM(s.total_amount) AS total_revenue
FROM Sales s
JOIN Products p ON s.product_id = p.product_id
GROUP BY p.name, p.category
ORDER BY total_revenue DESC;
```


| product_name  | category    | total_units_sold | total_revenue |
|---------------|-------------|------------------|---------------|
| Basketball    | Sports      | 61               | 289079        |
| Shoes         | Clothing    | 59               | 284498        |
| Chair         | Home        | 54               | 265518        |
| Smartwatch    | Electronics | 47               | 228561        |
| Sofa          | Home        | 55               | 218130        |
| Laptop        | Electronics | 47               | 210607        |
| Bed           | Home        | 66               | 201498        |
| Football      | Sports      | 53               | 199704        |
| Jeans         | Clothing    | 41               | 180113        |
| Tennis Racket | Sports      | 43               | 175784        |
| Cricket Bat   | Sports      | 37               | 131683        |
| Dress         | Clothing    | 49               | 130879        |
| Gym Gloves    | Sports      | 29               | 121742        |
| Lamp          | Home        | 56               | 120232        |
| Dining Table  | Home        | 53               | 118455        |
| Jacket        | Clothing    | 59               | 109268        |
| Tablet        | Electronics | 63               | 96390         |
| Headphones    | Electronics | 62               | 66092         |
| Smartphone    | Electronics | 38               | 45638         |
| T-Shirt       | Clothing    | 28               | 43428         |

