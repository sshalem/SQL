###### _

<img src="https://img.shields.io/badge/-6. Writing Complex Query %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[Sub Queries in the WHERE clause](#1)   |             |
|  2  |[IN / NOT IN  (Sub Query)](#2)   |  
|  3  |[SubQuery VS JOIN](#3)   | 
|  4  |[ALL keyword](#4)   | 
|  5  |[ANY / SOME keyword](#5)   | 
|  6  |[Correlated SubQueries](#6)   | 
|  7  |[EXISTS operator](#7)   | 
|  8  |[Sub Queries in the SELECT Clause](#8)   | 
|  9  |[Sub Queries in the FROM Clause](#9)   | 




--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-1. Sub Queries in the WHERE clause %20-blue" height=40px>

This is how we use SubQueris. </br>
We can use them in:
1. WHERE clause
2. in the FROM claue
3. in the SELECT clause itself

Let's look in the table of products , </br>

![image](https://user-images.githubusercontent.com/36256986/164946506-820813d9-41a7-41dd-a84c-1e1189a92c25.png)

### [Example 1](#-) 

Let's say I want to find all the products that thier **unit_price** is more than **Letucce** .

#### Query w/o SubQuery

```sql
SELECT * 
FROM products
WHERE unit_price > 3.35;
```

#### Query with SubQuery

```sql
SELECT * 
FROM products
WHERE unit_price > (
	SELECT unit_price 
    FROM products 
    WHERE name LIKE 'Lettuce%');
```

![image](https://user-images.githubusercontent.com/36256986/164946605-2305f4e0-b702-4d5f-9166-8ef507fc0bb3.png)

### [Exercise](#-) 

In **sql_hr** DB , find employees whose earn more than avg.

```sql
SELECT *
FROM employees 
WHERE salary > (
	SELECT 
		AVG(salary)
  FROM employees);
```



[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. IN / NOT IN  (Sub Query) %20-blue" height=40px>

Find the products that have NEVER been ordered.

```sql
SELECT *
FROM products
WHERE product_id NOT IN(
	SELECT DISTINCT product_id
	FROM order_items);
```

![image](https://user-images.githubusercontent.com/36256986/164947195-30ee4fc8-a4e1-4358-964c-76e9dc8defd2.png)

### [Exercise](#-) 

Find clients without invoices.

```sql
SELECT * 
FROM clients
WHERE client_id NOT IN(
	SELECT DISTINCT client_id 
	FROM invoices);
```

![image](https://user-images.githubusercontent.com/36256986/164947326-a6ccf6ff-bee3-4054-bba1-d5815708bf47.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-3. SubQuery VS JOIN  %20-blue" height=40px>

Quite often we can write a JOIN instead of a SubQuery.
We always need to take the better options for not making the query too complex. </br>
Thus, always pay attention for the readability of the code.

Both of these queries give same results.

```sql
SELECT * 
FROM clients
WHERE client_id NOT IN(
	SELECT DISTINCT client_id 
	FROM invoices);
    
SELECT * 
FROM clients
LEFT JOIN invoices USING(client_id)
WHERE invoice_id IS NULL;
```

### [Exercise](#-) 

Find customers who order letucce (id=3). </br>
Select customer_id, first_name, last_name.

both queries give same results, but the one with JOIN's is more readable.

```sql
--  WIth JOIN's
SELECT DISTINCT
    customer_id,
    first_name,
    last_name
FROM customers c
JOIN orders o USING(customer_id)
JOIN order_items oi USING(order_id)
WHERE oi.product_id = 3;

--  With SubQuery
SELECT 
    customer_id,
    first_name,
    last_name
FROM customers
WHERE customer_id IN(
    SELECT o.customer_id
    FROM orders o
    JOIN order_items oi USING(order_id)
    WHERE oi.product_id = 3);
```

![image](https://user-images.githubusercontent.com/36256986/164948067-56598e22-8715-4ca2-934e-071ce3e334c1.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 4

<img src="https://img.shields.io/badge/-4. ALL keyword %20-blue" height=40px>

Let's see with an example how to use the [**_ALL_**](#-) keyword.

Let's see how to find :
* invoices larger than all invoices of client 3.

```sql
SELECT 
    client_id,
    invoice_id,
    invoice_total
FROM invoices 
WHERE invoice_total > (    
	SELECT 	
	    MAX(invoice_total)
	FROM invoices
	WHERE client_id = 3);
```

![image](https://user-images.githubusercontent.com/36256986/164967658-d0211fd6-f6a0-4f95-a5e3-38a196a0bc81.png)

Another Way to write this code is using the **_ALL_** keyword which will give same results.</br>
[Question:](#-) </br>
How it works with the ALL keyword?

[Answer:](#-)</br>
the SubQuery will return al invoices of client_id 3 (for example :150 ,163, 158 ...)</br>
Since we have the ALL keyword, MySql will compare each invoice with the results in the subquery. </br>
For example : if we get 165, the ALL keyword will compare 165 with (150 ,163, 158 ...) , and If ALL applys then the result will be shown in the report.</br>
Then it will check the next invoice with ALL (150 ,163, 158 ...) etc...

```sql
SELECT 
    client_id,
    invoice_id,
    invoice_total
FROM invoices
WHERE invoice_total > ALL (
	SELECT invoice_total			
	FROM invoices
	WHERE client_id = 3);
```

Both implementations are good, both are readable.

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 5

<img src="https://img.shields.io/badge/-5. ANY / SOME keyword %20-blue" height=40px>

Let's see with an example how to use the [**_ANY_**](#-) keyword.

Let's see how to find :
* clients with at least 2 invoices.

The inner Query will return :

![image](https://user-images.githubusercontent.com/36256986/164969285-8c522ebb-094d-480a-8929-bb87db4152f8.png)


```sql
SELECT * 
FROM invoices
WHERE client_id IN (
    SELECT client_id		 
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >= 2)
ORDER BY client_id;
```

We can see that [= ANY](#-) is same as [IN](#-) operator

```sql
SELECT * 
FROM invoices
WHERE client_id = ANY (
    SELECT client_id		 
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >= 2)
ORDER BY client_id;;
```

For **ANY** client_id it will show the result.</br>
If client_id=1 , the count=5, than for ANY of 5 row it will show results.

![image](https://user-images.githubusercontent.com/36256986/164969330-c6c12f0a-ffe7-4bbb-81bb-4a11475e20bb.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 6

<img src="https://img.shields.io/badge/-6. Correlated SubQueries %20-blue" height=40px>

Lets look at the following request:
* Select employees whose salary is above the average in thier office.

When we use a [Correlated SubQuery](#-), this SubQuery gets executed for each row in the main query.</br>
For this reason [Correlated SubQuery](#-) can sometimes be slow.</br>
[Correlated SubQuery](#-) are very powerfull

```WHERE office_id = e.office_id``` using this line makes it a [Correlated SubQuery](#-).
I didn't use GROUP BY .
I can se [GROUP BY](#-) to find the AVG of each office, but I must use a [Correlated SubQuery](#-) to get this .

```sql
SELECT *
FROM employees e
WHERE salary > (
	SELECT AVG(salary)
	FROM employees
	WHERE office_id = e.office_id);
```

### [Exercise](#-) 

- Get invoices that are larger than the clients avg invoice amount.

```sql
SELECT *
FROM invoices i
WHERE invoice_total > (
    SELECT AVG(invoice_total)
    FROM invoices
    WHERE client_id = i.client_id);
```

![image](https://user-images.githubusercontent.com/36256986/164970721-17b4530f-7a8d-49b2-a145-f7173c06fda2.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 7

<img src="https://img.shields.io/badge/-7. EXISTS operator %20-blue" height=40px>

When we use the [**_IN_**](#-) operator , the SubQuery will retun a result from the WHERE clause.</br>
If the SubQuery we wrote after the [**_IN_**](#-) operator produces a large result set , </br>
It is more efficient to use the [**_EXISTS_**](#-) operator, because when we use the [**_EXISTS_**](#-) operator, the SubQuery doesn't actually return a result set to the outer query.

We can we are using a [Correlated SubQuery](#-) SubQuery when using the [**_EXISTS_**](#-) operator.

```sql
SELECT *
FROM clients
WHERE client_id IN(
    SELECT DISTINCT client_id
    FROM invoices);
```

```sql
SELECT *
FROM clients c
WHERE EXISTS (
    SELECT client_id
    FROM invoices
    WHERE client_id = c.client_id);
```

![image](https://user-images.githubusercontent.com/36256986/164971511-d59a2ba9-3835-401a-9d31-7336efc046ba.png)

### [Exercise](#-) 

Find products that have never been ordered.

solution using the [**_IN_**](#-) operator 

```sql
SELECT * 
FROM products 
WHERE product_id NOT IN (
    SELECT product_id
    FROM order_items);
```

solution using the [**_EXISTS_**](#-)operator 

```sql
SELECT * 
FROM products p
WHERE NOT EXISTS (
    SELECT product_id
    FROM order_items
    WHERE product_id = p.product_id);
```

![image](https://user-images.githubusercontent.com/36256986/164977057-3ee2f0b0-f064-4e44-be44-7a358cfb1d3e.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 8

<img src="https://img.shields.io/badge/-8. Sub Queries in the SELECT clause %20-blue" height=40px>

So far, in all examples above we used Sub Queries in the WHERE clause. </br>
In this section I will show how we can use Sub Queries in the SELECT clause. </br>

Let's say we want to generate a report that looks like this result:

![image](https://user-images.githubusercontent.com/36256986/164977408-06e30d48-d01e-4d45-9595-65ffa6b85f7c.png)

```sql
SELECT 
    invoice_id,
    invoice_total,
    (SELECT 
        AVG(invoice_total) 
	FROM invoices) AS invoice_average,
    (invoice_total - (SELECT AVG(invoice_total) FROM invoices)) AS difference
FROM invoices;

-- Modify code to be shorter in the difference field
SELECT 
    invoice_id,
    invoice_total,
    (SELECT AVG(invoice_total) 
        FROM invoices) AS invoice_average,
    invoice_total - (SELECT invoice_average) AS difference
FROM invoices;
```

### [Exercise](#-) 

Write a Query to produce this result.

![image](https://user-images.githubusercontent.com/36256986/164978064-9adac964-11a9-4107-b098-735714c5d0ac.png)

```sql
SELECT
    c.client_id,
    c.name,
    (SELECT SUM(invoice_total) 
     FROM invoices 
     WHERE client_id = c.client_id) AS total_sales,
    (SELECT AVG(invoice_total) FROM invoices) AS average,
    (SELECT total_sales - average) AS difference
FROM clients c;  
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 9

<img src="https://img.shields.io/badge/-9. Sub Queries in the FROM Clause %20-blue" height=40px>

Whenever we use SubQuery in the [**_FROM_**](#-) clause , we need to give it an ALIAS.

```sql
SELECT * 
FROM (SELECT
	c.client_id,
	c.name,
	(SELECT SUM(invoice_total) 
	 FROM invoices 
	 WHERE client_id = c.client_id) AS total_sales,
	(SELECT AVG(invoice_total) FROM invoices) AS average,
	(SELECT total_sales - average) AS difference
	FROM clients c) AS sales_summary
WHERE total_sales IS NOT NULL;
```

![image](https://user-images.githubusercontent.com/36256986/164981142-41113589-69ce-416f-90f4-3db1542d985a.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

