# Pizza-Sales-end-to-end-Data-Analysis-Project

## PROBLEM STATEMENT

Analyzed key indicators for our pizza sales data to gain insights into our business performance. Calculated the following metrics:

Total Revenue: The sum of the total price of all pizza orders.

QUERY : SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/cb5bc222-80a3-4f09-9337-52fd2f7f7e24)


Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

QUERY:SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/e191f524-7f2e-4e14-a0a9-9a5795b5063d)


Total Pizzas Sold: The sum of the quantities of all pizzas sold.

QUERY: SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/f955f058-8c10-4dfb-8a81-c30a55f9a739)


Total Orders: The total number of orders placed.

QUERY: SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/be27b1f2-f8bf-4640-a207-78f4e4797192)


Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

QUERY: SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/bd130ad3-ee4d-4d4b-9de6-a0fbafa6755d)


Visualized various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

Hourly Trend for Total Pizzas Sold:

SELECT DATEPART(HOUR, order_time) as order_hours, SUM(quantity) as total_pizzas_sold
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/25c6662e-0cd5-4f36-8088-6865b697bd61)


Created a stacked bar chart that displays the hourly trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a hourly basis.

2.Weekly Trend for Total Orders:

SELECT 
    DATEPART(ISO_WEEK, order_date) AS WeekNumber,
    YEAR(order_date) AS Year,
    COUNT(DISTINCT order_id) AS Total_orders
FROM 
    pizza_sales
GROUP BY 
    DATEPART(ISO_WEEK, order_date),
    YEAR(order_date)
ORDER BY 
    Year, WeekNumber;


![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/ee66a936-c3f6-45af-9db9-e172953a4776)
![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/1c7fb05d-1bdd-49ed-ae6a-8b6b617cd047)

Created a line chart that illustrates the weekly trend of total orders throughout the year. This chart will allow us to identify peak weeks or periods of high order activity.

3.Percentage of Sales by Pizza Category:

SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/0a18158d-0c38-47d1-8cde-06bc37dd58f0)

Created a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

4.Percentage of Sales by Pizza Size:

SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/af4a5e7b-9e1a-4272-9387-213fc06c2809)

Generated a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.


5.Total Pizzas Sold by Pizza Category:

SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/d5ae98d6-a5b6-4f09-99cb-30689d713c69)

Created a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

6.Top 5 Best Sellers by Revenue, Total Quantity and Total Orders

SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/ac037af2-07e7-409b-8bf1-1b631f455c35)



SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/61557467-202b-4eca-9c99-8e68101b5a1a)


SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/166a43a0-c2dd-463a-a544-e89fe849ed7b)


Created a bar chart highlighting the top 5 best-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.

7. Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders

SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/91260091-102e-489d-8c55-5d22e0f715b5)

SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/40bca372-afe8-459f-a105-14bea2eec0ec)

SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC


![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/0008aeea-d650-4abd-b6ec-864562cfce83)

Created a bar chart showcasing the bottom 5 worst-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will enable us to identify underperforming or less popular pizza options.

## DASHBOARD

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/f48a60c4-9bcd-4f0d-a536-30dfebcc28db)

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/75ff3f3f-c5dc-4145-a422-c85007d5fafb)

![image](https://github.com/farhan965/Pizza-Sales-end-to-end-Data-Analysis-Project/assets/116187483/6cccd54e-94d5-4dff-a09c-34bc36b78fbe)




## SOFTWARES USED:
MS OFFICE/ EXCEL

MS SQL SERVER

SQL SERVER MANAGEMENT STUDIO 

TABLEAU

AZURE DATA FACTORY

AZURE SYNAPSE

AZURE DATA BRICKS

AZURE DATA LAKE GEN 2

AZURE KEY VAULT










