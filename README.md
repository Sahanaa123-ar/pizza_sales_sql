# pizza_sales_sql
Retrieve the total number of orders placed?
 SELECT COUNT(order_id) AS total_orders FROM orders;

Calculate the total revenue generated from pizza sales?
 SELECT 
round(SUM(order_details.quantity*pizzas.price),2) AS total_sales
from order_details join pizzas
ON pizzas.pizza_id = order_details.pizza_id;

Identify the highest-priced pizza?
 SELECT pizza_types.name, pizzas.price
from pizza_types join pizzas
ON pizza_types.pizza_type_id=pizzas.pizza_type_id
ORDER BY pizzas.price DESC limit 1;

Identify the most common pizza size ordered?
 SELECT quantity,Count(order_details_id)
FROM order_details GROUP BY quantity;
SELECT pizzas.size, count(order_details.order_details_id) AS order_count
from pizzas join order_details
On pizzas.pizza_id = order_details.pizza_id
group by pizzas.size order by order_count desc;

Join the necessary tables to find the total quantity of each pizza category ordered?
 SELECT pizza_types.category,
SUM(order_details.quantity) AS quantity
FROM pizza_types join pizzas
ON pizza_types.pizza_type_id=pizzas.pizza_type_id
join order_details
ON order_details.pizza_id=pizzas.pizza_id
GROUP BY category order by quantity DESC;

Determine the distribution of orders by hour of the day?
 SELECT hour(order_time) AS hour,count(order_id) AS order_count from orders
group by hour(order_time);

Join relevant tables to find the category-wise distribution of pizzas?
  SELECT category, count(name) from pizza_types
group by category; 

Group the orders by date and calculate the average number of pizzas ordered per day?
  SELECT round(avg(quantity),0) from 
(SELECT orders.order_date, sum(order_details.quantity) AS quantity
from orders join order_details
on orders.order_id = order_details.order_id
group by orders.order_date) AS order_quantity;
