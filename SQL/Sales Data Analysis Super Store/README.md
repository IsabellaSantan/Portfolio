# Buisness Sales Analysis for Super Store Dataset 

## Sales

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


### How does discounting impact profit margins?
```sql
SELECT 
  Discount,
  COUNT(*) AS Transaction_Count,
  SUM(Sales) AS Total_Sales,
  SUM(Profit) AS Total_Profit,
  AVG(Profit) AS Avg_Profit,
  (SUM(Profit) / NULLIF(SUM(Sales), 0)) * 100 AS Profit_Margin_Percent
FROM sales_data
GROUP BY Discount
ORDER BY Discount;
```
| Discount | Transactions | Total Sales   | Total Profit  | Avg Profit | Profit Margin (%) |
|----------|--------------|---------------|---------------|------------|--------------------|
| 0.00     | 4798         | 1,087,908.47  | 320,987.88    | 66.900350  | 29.505045          |
| 0.10     | 94           | 54,369.30     | 9,029.21      | 96.055426  | 16.607185          |
| 0.15     | 52           | 27,558.59     | 1,418.98      | 27.288077  | 5.148957           |
| 0.20     | 3657         | 764,594.28    | 90,338.16     | 24.702806  | 11.815176          |
| 0.30     | 227          | 103,226.76    | -10,369.34    | -45.679912 | -10.045205         |
| 0.32     | 27           | 14,493.45     | -2,391.16     | -88.561481 | -16.498211         |
| 0.40     | 206          | 116,417.83    | -23,057.08    | -111.927573| -19.805454         |
| 0.45     | 11           | 5,484.98      | -2,493.12     | -226.647273| -45.453584         |
| 0.50     | 66           | 58,918.65     | -20,506.51    | -310.704697| -34.804786         |
| 0.60     | 138          | 6,644.68      | -5,944.64     | -43.077101 | -89.464654         |


## Product Performance

### Which products generate the highest revenue and profit?

```sql
SELECT 
  Product_name, 
  COUNT(*) AS occurrence
FROM sales_data
GROUP BY Product_name
ORDER BY occurrence DESC
LIMIT 10;
```
| Rank | Product Name                                                   | Occurrence |
|------|----------------------------------------------------------------|------------|
| 1    | Staple envelope                                                | 48         |
| 2    | Easy-staple paper                                              | 46         |
| 2    | Staples                                                        | 46         |
| 4    | Avery Non-Stick Binders                                        | 20         |
| 5    | Staples in misc. colors                                        | 19         |
| 6    | Staple remover                                                 | 18         |
| 6    | KI Adjustable-Height Table                                     | 18         |
| 8    | Storex Dura Pro Binders                                        | 17         |
| 9    | Staple-based wall hangings                                     | 16         |
| 10   | Logitech 910-002974 M325 Wireless Mouse for Web Scrolling     | 15         |








