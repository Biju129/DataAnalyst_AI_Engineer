# Data Analyst Preparation KIT

## 1 . Python Basics

> Logic and Data Manipulation with Python

List - is a collection of similar data types and it can have nested lists,dictionaries and so on..

Dictionaries - is a {Key:Value} pair of data where key is immutable (similar to hash map in Java).

First coding with the basic python language without pandas.

    SAMPLE DATA

    sales = [
        {"product": "Laptop", "price": 50000, "quantity": 2},
        {"product": "Phone", "price": 20000, "quantity": 5},
        {"product": "Tablet", "price": 15000, "quantity": 3},
        {"product": "Laptop", "price": 50000, "quantity": 1},
        {"product": "Phone", "price": 20000, "quantity": 2}
    ]

1. Calculate the total revenue of all sales.

        total_revenue =0
        for i in sales:
        total_revenue+= i.get("price") * i.get("quantity")

        print(total_revenue)

2. Find the product with the highest total revenue.

        product_revenue ={}

        for i in sales:
            product = i.get("product")
            price = i.get("price")
            revenue = i.get("price")*i.get("quantity")

            if product in product_revenue:
                product_revenue[product] += revenue
            else:
                product_revenue[product] = revenue


        print(max(product_revenue))

3. Calculate the total quantity sold for each product.

        product_quantity = {}

        for i in sales:
            product = i.get("product")
            quantity = i.get("quantity")

            if product in product_quantity:
                product_quantity[product] += quantity
            else:
                product_quantity[product] = quantity

        print(product_quantity)

4. Additional Challenge : print the product name and revenue, e.g. Laptop — ₹150000. 

        product_revenue ={}

        for i in sales:
            product = i.get("product")
            price = i.get("price")
            revenue = i.get("price")*i.get("quantity")

            if product in product_revenue:
                product_revenue[product] += revenue
            else:
                product_revenue[product] = revenue


        print(product_revenue)

**Summary**
___
We have learnt to breakdown the question requirements along we learnt to use dictionary's get() and aggregate functions like max() sum().  

## 2. SQL Basics for Data Analysis

> Topics


| Topic | Focus |
| --- | --- | 
| 1 | GROUP BY + aggregate functions |
| 2 | Join |
| 3 | HAVING vs WHERE|
| 4 | Subqueries |
| 5 | Window functions (RANK, ROW_NUMBER) |

* Task 1 — GROUP BY + Aggregation


        SELECT product, sum(price*quantity) as total_revenue 
        FROM sales
        GROUP BY product
        ORDER BY total_revenue desc;
 
 Concept mastered: GROUP BY + SUM + ORDER BY

 ---

* Task 2 — WHERE vs HAVING

        SELECT product, SUM(price * quantity) AS total_revenue
        FROM sales
        GROUP BY product
        HAVING total_revenue > 40000
        ORDER BY total_revenue DESC;

The use of HAVING total_revenue is supported in PostgreSQL and MySQL.

---

* Task 3 — JOIN

        SELECT c.name, SUM(o.amount) AS total_amount
        FROM customers c
        LEFT JOIN orders o ON c.customer_id = o.customer_id
        GROUP BY name
        ORDER BY total_amount DESC;

* Task 4 — WHERE vs HAVING (interview-level)

        SELECT c.name, SUM(o.amount) AS total_amount
        FROM orders o
        LEFT JOIN customers c 
            ON c.customer_id = o.customer_id
        GROUP BY c.name, c.customer_id
        HAVING SUM(o.amount) > 4000;

---

> Using Ranks 

        Syntax :

        RANK() OVER (
        [PARTITION BY expression, . . . ]
        ORDER BY expression (ASC | DESC) );


---

* Window Functions
* Task 5 — Find the 3nd highest from the table using Ranks

        WITH ranked_orders AS (
            SELECT amount,
                DENSE_RANK() OVER (ORDER BY amount DESC) AS rnk
            FROM orders
        )
        SELECT amount
        FROM ranked_orders
        WHERE rnk = 2;

## 2. Excel and Data Cleaning

1. Missing values
2. Duplicate records
3. Filtering & sorting
4. Excel formulas
5. Pivot tables

|Employee|	Department|	Salary|
|-----|----|------|
|Arun	|IT|	35000|
|Priya	|HR|	40000|
|Arun|	IT|	35000|
|Karthik|	IT|	NULL|
|Divya	|HR	|45000|

* Which rows are duplicates, and how would you handle the missing salary?

        Duplicate:
        Arun – IT – 35000 → remove the repeated row.
        
        Missing salary (Karthik):        
        Either fill it with the correct value or exclude it, depending on the analysis.

* Calculate the average salary.

        =AVERAGE(C2:C6)

* Count employees belonging to IT.

        =COUNTIF(B2:B6,"IT")

* Find the highest salary.

        =MAX(C2:C6)

* Calculate total salary paid to HR employees.

        =SUMIF(B2:B6,"HR",C2:C6)

## Staistics and Business Thinking

>Topics
1. Mean vs Median
2. Outliers
3. Correlation
4. Business KPIs

Mean (**AVERAGE**) -> Sum (All Values) / Total Number of Values.
**Median** -> Middle Most Value

**What should a Data Analyst conclude?**

If the mean is much higher than the median because one unusually large sale (₹10,000) pulls the average upward.

### OUTLIERS

An outlier is a data point that is unusually far from the rest of the values.

    In our sales data:

    1000, 1200, 1500, 1800, 10000

Here **₹10,000** is the outlier.

### CORRELATION

Correlation helps us understand whether two variables move together.

|Type|	Meaning|	Example|
|----|------|------|
|Positive correlation|	Both increase together|	Advertising spend ↑, Sales ↑|
|Negative correlation|	One increases, the other decreases	|Price ↑, Demand ↓|
|No correlation|	No consistent relationship	|Shoe size vs. monthly sales|

_**Remember**: Correlation does not mean causation. Just because two things move together doesn't mean one caused the other._

> Task Questions

|Advertising Spend (₹)	| Sales (₹)|
|----|-----|
|1,000	|10,000|
|2,000	|18,000|
|3,000	|25,000|
|4,000	|35,000|
|5,000	|45,000|

1. What type of correlation do you observe?

        You observed a positive correlation: as advertising spending increases, sales also increase.


2. Can the business conclude that increasing advertising always causes sales to increase? Why or why not?

        The data shows a positive correlation between advertising expenditure and sales. However, we cannot conclude that advertising alone causes sales to increase. Other factors, such as seasonality, market demand and competition, may also influence sales. Further analysis is required to determine the actual impact of advertising.

![Correlation Image](https://chatgpt.com/s/i_6b07e6b12ddc8191a03ac40bf3522e28)

---

### KPI Key Performance Indicator

|Business goal|	KPI|
|-----|-----|
|Increase sales	|Total revenue|
|Attract customers|	Customer acquisition|
|Improve website|	Conversion rate|
|Retain customers|	Retention rate|
|Reduce expenses|	Cost per acquisition|

> Task 

An online store has the following data for one month:
- Visitors: 10,000
- Orders: 500
- Revenue: ₹5,00,000
- Advertising spend: ₹50,000

1. Conversion Rate (%)      
> $\frac{\text{Orders}}{\text{Visitors}}\times100$

2. Average Order Value (AOV)        
> $\frac{\text{Revenue}}{\text{Orders}}$

3. ROAS (Return on Ad Spend)        
> $\frac{\text{Revenue}}{\text{Advertising Spend}}$

        1. Conversion Rate is 5%
        2. AOV is 1,000
        3. ROAS is 10
        10× ROAS does not mean 10× profit. Revenue isn't profit — product costs, shipping, salaries and other expenses still need to be deducted.

## 4. Power BI & Data Visualization

        Your manager wants to understand how revenue changes over time and identify the sales trend from January to May.

        A line chart is ideal for showing trends over time. Here, the X-axis represents months and the Y-axis represents revenue.

Why not the others?
- Pie/Donut → Show proportions or composition, not trends over time.
- Card → Displays a single KPI, such as total revenue.
- Line chart → Shows increases, decreases and trends over time.

> POWER QUERY EDITOR

Power Query is the data preparation layer of Power BI. It helps you clean and reshape data before it enters your data model.

Typical operations:
- Remove duplicate rows
- Handle missing values
- Change data types (Text → Date, Text → Number)
- Rename columns
- Filter unwanted records
- Merge or append datasets

_I use Power Query Editor for ETL (Extract, Transform, Load). It helps clean, transform and structure raw data before building reports and visualizations._

> DAX & Measures
Now let's learn a very important distinction.

**In Power BI, DAX (Data Analysis Expressions) is used to create calculations, measures and analytical logic.**

SUMX is an iterator. It evaluates an expression for each row of a table and then sums the resulting values.

> Data Storytelling

A dashboard is not just a collection of charts. It should tell the manager what happened, why it matters, and what action to take.

Your sales dashboard reveals:
- Revenue increased by 30% this month.
- Laptop sales contributed 60% of total revenue.
- Phone sales declined by 20%.

        What you did well
        - Identified laptops as the strongest revenue contributor.
        - Noticed phone sales declining by 20%.
        - Suggested advertising as a possible way to recover phone sales.
        - Recommended sustaining laptop performance while improving phones.

        One refinement: Revenue contribution doesn't necessarily mean laptops are being sold in greater quantities. It could also mean their unit price is higher. Before increasing ad spend on phones, investigate why sales declined.

