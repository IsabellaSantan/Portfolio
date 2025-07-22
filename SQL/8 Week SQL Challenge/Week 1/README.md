# 🍜 Case Study #1: Danny's Diner
![image](https://github.com/user-attachments/assets/3ae0ae77-f24f-4851-bcbc-7f898979c60d)



## 📚 Table of Contents
Business Task
Entity Relationship Diagram
Question and Solution
Please note that all the information regarding the case study has been sourced from the following link: [here] (https://8weeksqlchallenge.com/case-study-1/).

## Business Task
Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite.

## Entity Relationship Diagram

![image](https://github.com/user-attachments/assets/15b755f7-58ab-4590-8398-c74a76d77864)

# Question and Solution

## 1. What is the total amount each customer spent at the restaurant?

``` sql
SELECT sales.customer_id, SUM(menu.price) AS Money_Spent
FROM sales
INNER JOIN menu 
ON sales.product_id = menu.product_id
GROUP BY sales.customer_id
ORDER BY SUM(menu.price) DESC;
```
*Results*
| customer_id  | Money_Spent |
| ------------- | ------------- |
| A  | 76  |
| B | 74  |
| C | 36  |

## 2. How many days has each customer visited the restaurant?
``` sql
SELECT customer_id, COUNT(DISTINCT order_date) AS days_visited
FROM sales
GROUP BY customer_id;
 ```

*Results*
| customer_id  | Money_Spent |
| ------------- | ------------- |
| A  | 4  |
| B | 6  |
| C | 2  |

## 3.What was the first item from the menu purchased by each customer?

``` sql
SELECT DISTINCT sales.customer_id, menu.product_name
FROM sales
LEFT JOIN menu ON sales.product_id = menu.product_id
WHERE sales.order_date = (
  SELECT MIN(order_date)
  FROM sales AS s2
  WHERE s2.customer_id = sales.customer_id
);
```
*Results*
| customer_id | product_name |
|-------------|--------------|
| A           | sushi        |
| A           | curry        |
| B           | curry        |
| C           | ramen        |

## 4.What is the most purchased item on the menu and how many times was it purchased by all customers?
``` sql
SELECT m.product_name, COUNT(s.product_id) AS total_purchases
FROM sales AS s
INNER JOIN menu AS m ON s.product_id = m.product_id
GROUP BY m.product_name
ORDER BY total_purchases DESC
LIMIT 1;
```
| product_name | total_purchases |
|--------------|-----------------|
| Ramen        | 8               |

## 5.Which item was the most popular for each customer?

``` sql
SELECT customer_id, product_name, times_ordered
FROM (
  SELECT 
    s.customer_id, 
    m.product_name, 
    COUNT(*) AS times_ordered,
    RANK() OVER (PARTITION BY s.customer_id ORDER BY COUNT(*) DESC) AS rnk
  FROM sales AS s
  INNER JOIN menu AS m ON s.product_id = m.product_id
  GROUP BY s.customer_id, m.product_name
) ranked_orders
WHERE rnk = 1;
```
| Customer | Product | Times Ordered |
|----------|---------|----------------|
| A        | ramen   | 3              |
| B        | curry   | 2              |
| B        | sushi   | 2              |
| B        | ramen   | 2              |
| C        | ramen   | 3              |

```
