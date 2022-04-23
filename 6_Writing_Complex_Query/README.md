###### _

<img src="https://img.shields.io/badge/-6. Writing Complex Query %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[Sub Queries](#1)   |             |
|  2  |[IN / NOT IN  (Sub Query)](#2)   |  
|  3  |[x](#3)   | 



--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-1. Sub Queries %20-blue" height=40px>

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

#### [Exercise](#-) 

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

#### [Exercise](#-) 

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

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
