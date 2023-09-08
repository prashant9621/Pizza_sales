# Pizza_sales



# Problem Statement

Our business needs to gain valuable insights into our pizza sales data to improve our overall performance. Specifically, we aim to analyze the following key performance indicators (KPIs):

## Key Performance Indicators (KPIs)

1. [ ] **Total Revenue**: 💰 Calculate the sum of the total price of all pizza orders.

2. [ ] **Average Order Value**: 📦 Determine the average amount spent per order by dividing the total revenue by the total number of orders.

3. [ ] **Total Pizzas Sold**: 🍕 Calculate the sum of the quantities of all pizzas sold.

4. [ ] **Total Orders**: 📊 Count the total number of orders placed.

5. [ ] **Average Pizzas per Order**: 🍽️ Find the average number of pizzas sold per order by dividing the total number of pizzas sold by the total number of orders.

# Problem Statement

## Charts Requirement

We would like to visualize various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

1. [ ] **Daily Trend for Total Orders:**
   - 📊 Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

2. [ ] **Monthly Trend for Total Orders:**
   - 📈 Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

3. [ ] **Percentage of Sales by Pizza Category:**
   - 🍕 Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

4. [ ] **Percentage of Sales by Pizza Size:**
   - 🍕 Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

5. [ ] **Total Pizzas Sold by Pizza Category:**
   - 📊 Create a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

6. [ ] **Top 5 Best Sellers by Revenue, Total Quantity, and Total Orders:**
   - 🥇 Create a bar chart highlighting the top 5 best-selling pizzas based on Revenue, Total Quantity, and Total Orders. This chart will help us identify the most popular pizza options.

7. [ ] **Bottom 5 Best Sellers by Revenue, Total Quantity, and Total Orders:**
   - 🥉 Create a bar chart showcasing the bottom 5 worst-selling pizzas based on Revenue, Total Quantity, and Total Orders. This chart will enable us to identify underperforming or less popular pizza options.
  
# Pizza Sales SQL Queries

Here are the SQL queries to analyze our pizza sales data:

## A. KPIs
1. [ ] **Total Revenue**: Calculate the total revenue.

```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

Average Order Value: Determine the average order value.
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;

 Total Pizzas Sold: Calculate the total number of pizzas sold.
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
 Total Orders: Count the total number of orders placed.
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
Average Pizzas Per Order: Find the average number of pizzas sold per order.
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_per_order
FROM pizza_sales;


B. Daily Trend for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
C. Monthly Trend for Orders
SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date);
D. % of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
E. % of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
F. Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
G. Top 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
H. Bottom 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;
Top 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;
J. Bottom 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
K. Top 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;
L. Bottom 5 Pizzas by Total Orders
sql
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
























