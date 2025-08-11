# Pizza_Sales

# Data Portfolio: SQL - EXCEL







# Table of contents 

- [Objective](#objective)
- [Data Source](#data-source)
- [Design](#design)
 - [Tools](#tools)
- [Development](#development)
   - [Data Exploration](#data-exploration)
  - [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)
  - [Create the SQL View](#create-the-sql-view)
- [Visualization](#visualization)
- [Conclusion](#conclusion)




# Objective 

- What is the key Main point? 

The Head of Marketing wants to analyze key indicators for our pizza sales data to gain insights into the business performance


- What is the ideal solution? 

To create a dashboard that provides insights into the Pizzza Sales that includes their 
- Daily Trend for Total Orders
- Hourly Trend for Total Orders
- Percentage of Sales by Pizza Category
- Percentage of Sales by Pizza Size
- Total Pizzas Sold by Pizza Category
- Top 5 Best Sellers by Total Pizzas, and
- Bottom 5 Worst Sellers by Total Pizzas Sold


This will help the marketing team make informed decisions about which Pizza size, catgory that makes the highest and also lowest sales.
## User story 

As the Head of Marketing, I want to use the dashboard of the company Pizza Sales. 

This dashboard should allow me to identify the top performing Pizza and low performing based on metrics like Total Pizzas Sold by Pizza Category, Bottom 5 Worst Sellers by Total Pizzas Sold. 

With this information, I can make more informed decisions about which Pizza category/size, and therefore maximize which pizza to focus and which needs improvement or which to discard.


# Data source 

- Where is the data coming from? 
The data is sourced from Kaggle (an Excel extract)


# Stages

- Design
- Developement
- Testing
- Analysis 
 




## Tools 


| Tool | Purpose |
| --- | --- |
| Power BI | Exploring the data, Visualizing the data via interactive dashboards |
| SQL Server | Cleaning, testing, and analyzing the data |
| GitHub | Hosting the project documentation and version control |



# Development

## Pseudocode

- What's the general approach in creating this solution from start to finish?

1. Get the data
2. Explore the data in Excel
3. Load the data into SQL Server
4. Clean the data with Excel
5. Test the data with SQL
6. Visualize the data in Power BI
7. Generate the findings based on the insights
8. Write the documentation + commentary
9. Publish the data to GitHub Pages

## Data exploration notes

This is the stage where you have a scan of what's in the data, errors, inconcsistencies, bugs, weird and corrupted characters etc  


- What are your initial observations with this dataset? What's caught your attention so far? 

1. There are at least 13 columns that contain the data we need for this analysis, which signals we have everything we need from the file without needing to contact the client for any more data. 
2. We have more data than we need.




## Data cleaning 
- What do we expect the clean data to look like? (What should it contain? What contraints should we apply to it?)

The aim is to refine our dataset to ensure it is structured and ready for analysis. 

The cleaned data should meet the following criteria and constraints:

- Only relevant columns should be retained.
- All data types should be appropriate for the contents of each column.
- No column should contain null values, indicating complete data for all records.

Below is a table outlining the constraints on our cleaned dataset:

| Property | Description |
| --- | --- |
| Number of Rows | 48620 |
| Number of Columns | 14 |


- What steps are needed to clean and shape the data into the desired format?

1. Remove unnecessary columns by only selecting the ones you need
2. Extract Youtube channel names from the first column
3. Rename columns using aliases
4. CHANGE 
M-MEDIUM
L-LARGE
S-REGULAR
XXL-XX-LARGE
XL-X-LARGE








### Transform the data 





## Analyze key Indicators 
### SQL query 
```sql

-- 1. Total Revenue :
SELECT SUM(total_price) AS total_revenue
	FROM pizza_sales11




-- 2. Average Order Value : 
	SELECT SUM(total_price)/ COUNT (DISTINCT order_id) AS average_order_value 
	  FROM pizza_sales11


-- 3.Total Pizza Sold: 
	SELECT SUM(quantity) AS total_pizza_sold
	FROM pizza_sales11

-- 4) Total Orders: 
	SELECT COUNT(DISTINCT order_id) AS total_order  
	FROM pizza_sales11

-- 5) Average Pizzas Per Order:
	 SELECT CAST (SUM(quantity) AS DECIMAL (10,2)) /
	 CAST (COUNT(DISTINCT order_id) AS decimal (10,2)) AS avg_pizza_per_order
	 FROM pizza_sales11

CHARTS RQUIREMENT

We would like to visualize various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

-- 1) Daily Trend for Total Orders: 
	SELECT DATENAME(DW, order_date) AS order_day, 
	COUNT(DISTINCT order_id) AS Total_orders
	FROM pizza_sales
	GROUP BY DATENAME(DW, order_date)

-- 2) Hourly Trend for Total Orders: 
	SELECT DATEPART(HOUR, order_time) AS Order_Hours,
	COUNT(DISTINCT order_id) AS Total_orders
	FROM pizza_sales
	GROUP BY DATEPART(HOUR, order_time)
	ORDER BY DATEPART(HOUR, order_time)

-- 3) Percentage of Sales by Pizza Category: 
	SELECT pizza_category,SUM(total_price) AS Total_Sales,SUM(total_price) * 100 /(SELECT SUM(total_price)  FROM pizza_sales) 
	AS PCT_total_sales FROM pizza_sales 
	GROUP BY pizza_category 


-- 4) Percentage of Sales by Pizza Size: 
	SELECT pizza_size, SUM (total_price) AS Total_Sales,SUM(total_price) * 100 /(SELECT SUM(total_price)  FROM pizza_sales) 
	AS PCT_total_sales FROM pizza_sales 
	GROUP BY pizza_size

-- 5) Total Pizzas Sold by Pizza Category: 
	SELECT pizza_category, SUM(quantity) AS total_pizza_sold
	FROM pizza_sales 
	GROUP BY pizza_category

-- 6) Top 5 Best Sellers by Total Pizzas Sold: 
	SELECT TOP 5  pizza_name, SUM(quantity) AS total_pizza_sold
	FROM pizza_sales 
	GROUP BY pizza_name
	ORDER BY SUM(quantity) DESC

-- 7) Bottom 5 Worst Sellers by Total Pizzas Sold: 
	SELECT TOP 5  pizza_name, SUM(quantity) AS total_pizza_sold
	FROM pizza_sales 
	GROUP BY pizza_name
	ORDER BY SUM(quantity) ASC


```
# TOTAL_REVENUE
![Total Revenue](Document/Total%20Revenue.png)
# Average_ORDER_VALUE :
![Average_order_value](Document/Avg%20Order%20Value.png)
# Total Pizza Sold: 
![Total Pizza Sold](Document/Total%20Pizza%20Sold.png)
# TOTAL_ORDERS
![Total Orders](Document/Total%20Order.png)
# AVEREAGE_PIZZA_ORDER
![Average pizza order](Document/Avg%20Pizza%20per%20ord.png)


# Visualization 


## Results

- What does the dashboard look like?

![Excel Dashboard](Document/Pizza%20Dashboard.png)
 




# Analysis 

## Findings

- What did we find?
- Days
  - Orders are highest on Thursdays/Fridays/Saturday evenings
- Times
  - There are maximum orders from 12-01pm & after 4-8pm
- CATEGORY
  - Classic Category contributes to maximum sales & total order 
- SIZE
  - Large size pizza contribute to maximum sales
- BEST
  - Classic Deluxe & Chicken Pizzas are the sellers and revenue generators
- WORST
  - The Brie Carre  is at the bottom in both orders and revenue
