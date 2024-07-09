# Restaurant-Order-Analysis
Data Analyst Portfolio Project: Restaurant Order Analysis in SQL.
Data Analysis Portfolio Projects :

Restaurant Order Analysis:

1. RESTAURANT OPERATIONS ANALYSIS

THE
SITUATION

You've just been hired as a Data Analyst for the Taste of the World Café, a
restaurant that has diverse menu offerings and serves generous portions

THE
ASSIGNMENT

The Taste of the World Cafe debuted a new menu at the start of the year
You've been asked to dig into the customer data to see which menu items
are doing well / not well and what the top customers seem to like best

THE
OBJECTIVES

1. Explore the menu_items table to get an idea of what's on the new menu
2. Explore the order_details table to get an idea of the data that's been collected
3. Use both tables to understand how customers are reacting to the new menu.

OBJECTIVE 1: EXPLORE THE ITEMS TABLE

1. View the menu_items table and write a query to find the number of items on the menu.


Ans: 
    select * from menu_items;
    select count(*) from menu_items;


2. What are the least and most expensive items on the menu?

Ans:
    select *  from menu_items order by price ;
    select *  from menu_items order by price Desc;
    

3. How many Italian dishes are on the menu? What are the least and most expensive Italian dishes on the menu?

Ans:
    select count(*) from menu_items where category = 'italian';
    select * from menu_items where category = 'Italian' order by price;
    select * from menu_items where category = 'Italian' order by price desc;

4. How many dishes are in each category? What is the average dish price within each category?

Ans:
    select category, count(menu_item_id) as num_dishesh from menu_items group by category;
    select category, avg(price) as avg_price from menu_items group by category;


OBJECTIVE 2: EXPLORE THE ORDERS TABLE :

1. View the order_details table. What is the date range of the table?

Ans:
    select * from order_details;
    select * from order_details order by order_date; 
              OR
    select min(order_date), max(order_date) from order_details;


2. How many orders were made within this date range? How many items were ordered within this date range?

Ans:
    select count(distinct order_id) from order_details;
    select count(*) from order_details; 

3. Which orders had the most number of items?

Ans:
    select order_id, count(item_id) as num_item from order_details group by order_id order by num_item desc;

4. How many orders had more than 12 items?

Ans:
    select count(*) from (select order_id, count(item_id) as num_item from order_details group by order_id having num_item > 12) as num_order;


OBJECTIVE 3: ANALYZE CUSTOMER BEHAVIOR

1. Combine the menu_items and order_details tables into a single table.

Ans:
    select * from menu_items;
    select * from order_details;
    select * from order_details od left join menu_items im on od.item_id = mi.menu_item_id;

2. What were the least and most ordered items? What categories were they in?

Ans:
    select item_name, category , count(order_id) as num_purchase from order_details od left join menu_items im on od.item_id = mi.menu_item_id group by item_name , category  order by num_purchase desc;

3. What were the top 5 orders that spent the most money?

Ans:
    select order_id , sum(price) as total_spend from order_details od left join menu_items mi on od.item_id = mi.menu_item_id group by order_id order by total_spend desc limit  5;

4. View the details of the highest spend order. What insights can you gather from the results?

Ans:
    select category, count(item_id) as num_items from order_details od left join menu_items mi on od.item_id = mi.menu_item_id where order_id = 440 group by category;

5. View the details of the top 5 highest spend orders. What insights can you gather from the results?

Ans:
    select order_id, count(item_id) as num_items from order_details od left join menu_items mi on od.item_id = mi.menu_item_id where order_id in (440 , 2075, 1957, 330,2675) group by order_id;

## Authors

- [@https://github.com/KIsmail23](https://www.github.com/https://github.com/KIsmail23)


