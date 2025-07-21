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

```sql
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
