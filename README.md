<img width="915" height="500" alt="Pizza" src="https://github.com/user-attachments/assets/9d2ad2a0-74e4-4d34-9b36-82494add0eb1" />
<img width="900" height="498" alt="pizz 2" src="https://github.com/user-attachments/assets/f55b1068-ff34-4d43-953f-7b7b4ca0522e" />
# Pizza_Sales_Dashbord
This is a sales report on pizza in the United States

```sql
Key_Performance_Indicators (KPIs)

-- 1. Total Revenue
SELECT SUM(Total_price) AS Total_Revenue
FROM pizza_sales;

-- 2. Average Order Value
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Avg_order_Value
FROM pizza_sales;

-- 3. Total Pizzas Sold
SELECT SUM(quantity) AS Total_Pizz_Sold
FROM pizza_sales;

-- 4. Total Orders Placed
SELECT COUNT(DISTINCT order_id) AS Total_Orders 
FROM pizza_sales;

-- 5. Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_pizza_per_order
FROM pizza_sales;
```
```sql
Charts & Trends

-- 1. Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS Total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);

-- 2. Monthly Trend 
SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_orders 
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date) 
ORDER BY Total_orders DESC;

-- 3. Percentage Sales by Pizza Category
SELECT pizza_category, SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS PCT_Sales
FROM pizza_sales
GROUP BY pizza_category;

-- 4. Percentage of Sales by Pizza Size
SELECT pizza_size, SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS PCT_Sales
FROM pizza_sales
GROUP BY pizza_size;

-- 5. Top 5 Best Sellers (by Revenue)
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;

-- 6. Bottom 5 Worst Sellers (by Quantity)
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Quantity
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity ASC;

-- 7. Top 5 Best Sellers (by Quantity)
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Quantity
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity DESC;
```
