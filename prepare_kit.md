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
