# Buisness Sales Analysis for Super Store Dataset 

Question 1
### What is the total sales and profit over time?
```sql
SELECT 
SUM(Profit) AS Profit_over_Time, SUM(sales) AS Total_sales
FROM 
sales_data;
```
#### Results
| Profit Over Time | Total Sales   |
|------------------|---------------|
| $286,397.79      | $2,297,201.07 |

### What are the most profitable product categories and subcategories?

#### Most Profitable Subcategories 
``` sql

SELECT Category, Sub_Category, SUM(Profit) AS Total_Profit
FROM sales_data
GROUP BY Category, Sub_Category
ORDER BY Total_Profit DESC
LIMIT 3;
```
| Category         | Total Profit   |
|------------------|----------------|
| Technology       | $145,455.66    |
| Office Supplies  | $122,490.88    |
| Furniture        | $18,451.25     |

#### Most Profitable Categories

``` sql

SELECT Category ,Sub_category ,SUM(Profit) AS Total_Profit
FROM sales_data
GROUP BY Category, Sub_category
ORDER BY Total_Profit DESC
LIMIT 5;

```

| Category         | Sub_Category | Total Profit   |
|------------------|--------------|----------------|
| Technology       | Copiers      | $55,617.90     |
| Technology       | Phones       | $44,516.25     |
| Technology       | Accessories  | $41,936.78     |
| Office Supplies  | Paper        | $34,053.34     |
| Office Supplies  | Binders      | $30,221.64     |


#### Are there regions or segments operating at a loss?

#### States that are operating at a loss

``` sql
SELECT State, SUM(PROFIT) AS Profits FROM sales_data
GROUP BY State
HAVING Profits < 0
ORDER BY PROFITs ASC;
```

| State           | Total Profit (Loss) |
|-----------------|---------------------|
| Texas           | -$25,729.29         |
| Ohio            | -$16,971.37         |
| Pennsylvania    | -$15,560.04         |
| Illinois        | -$12,607.89         |
| North Carolina  | -$7,490.81          |
| Colorado        | -$6,527.86          |
| Tennessee       | -$5,341.66          |
| Arizona         | -$3,427.87          |
| Florida         | -$3,399.25          |
| Oregon          | -$1,190.48          |

