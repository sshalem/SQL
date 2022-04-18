###### _

<img src="https://img.shields.io/badge/-3. JOIN UNION USING clause %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[Retrieving Data From Multiple Tables](#1)   |	     |
|  2  |[INNER JOIN (or Just JOIN)](#2)   |		     |
|     |2.1                               |[JOIN](#2-1)       |
|     |2.2				 |[ALIAS with JOIN](#2-2)    |
|     |2.3				 |[JOIN across Database's](#2-3)   |
|     |2.4				 |[SELF JOINS (INNER)](#2-4)   | 
|     |2.5				 |[JOIN more the 2 tables](#2-5)   | 
|  2.6|[JOIN](#2-6)   |
|  3  |[OUTER JOIN (or Just JOIN)](#3)   | 
|  3.1|[JOIN](#3-1)   | 
|  3.2|[JOIN](#3-2)   | 
|  3.3|[JOIN](#3-3)   | 
|  3.4|[JOIN](#3-4)   | 
|  3.5|[JOIN](#3-5)   | 
|  3.6|[JOIN](#3-6)   |
|  5  |[UNION](#)   | 
|  3  |[USING CLAUSE](#-)   | 


--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-Retrieving Data From Multiple Tables.  %20-blue" height=40px>

Most of time we query columns from **multiple tables**. </br>
There are several type of JOIN:

	1. JOIN
	2. SELF JOIN
	3. INNER JOIN
	4. OUTER JOIN
	5. FULL JOIN
	6. LEFT JOIN
	7. RIGHT JOIN

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. INNER JOIN (or Just JOIN) %20-blue" height=40px>

**Question:**</br>
* What's the difference between **_INNER JOIN_** and **_JOIN_** in MySql?</br>

**Answer:**</br>
* **There is no difference** , the **INNER** key is optional so we don't have to type it.</br>

I will show examples using the tables , customers and order.

### [Orders table](#-)

![image](https://user-images.githubusercontent.com/36256986/163826156-fa1919f6-8c04-4e15-a4fb-c3003e7833d6.png)


### [Customers table](#-)

![image](https://user-images.githubusercontent.com/36256986/163826170-6e037da9-0daf-4912-9fc3-423ea20a71d1.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-1

<img src="https://img.shields.io/badge/-2.1. JOIN %20-yellow" height=30px>

Let's run the following query.

on tables of orders & customers FROM section 2).

```sql
SELECT * 
FROM orders 
JOIN customers 
	ON orders.customer_id = customers.customer_id;
```

We got a joined table with all the columns of of both tables (orders & customers).

![image](https://user-images.githubusercontent.com/36256986/163826955-41e078bc-e47e-4341-a3c8-d692753fc780.png)

Let's make it more clear and select only 3 columns form both tables:

```sql
SELECT 
    order_id, 
    first_name, 
    last_name  
FROM orders 
JOIN customers 
	  ON orders.customer_id = customers.customer_id;
```

![image](https://user-images.githubusercontent.com/36256986/163827270-e85d06eb-3940-4a28-b9f3-637fc0a9a4fd.png)

if we want to add also the customer_id column , we must add  a prefix from which table to add it, Since it is ambiguous. </br>
See example in the query below: 

```sql
SELECT 
    order_id, 
    orders.customer_id, 
    first_name, 
    last_name  
FROM orders 
JOIN customers 
	  ON orders.customer_id = customers.customer_id;
```

![image](https://user-images.githubusercontent.com/36256986/163827557-54618407-c896-4bd2-81ce-74bbe8044c72.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-2

<img src="https://img.shields.io/badge/-2.2. ALIAS with JOIN  %20-yellow" height=30px>

We can add ALIAS when doing JOIN in the query. </br>
By convention we **_abbreviate the tables_** name.

Let's take the following query and add it ALIAS by convention:

code w/o ALIAS:

```sql
SELECT 
	order_id, 
	orders.customer_id, 
	first_name, 
	last_name  
FROM orders 
JOIN customers 
	ON orders.customer_id = customers.customer_id;
```

same code with ALIAS:

```sql
SELECT 
	order_id, 
	o.customer_id, 
	first_name, 
	last_name 
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id;
```

This is much cleaner code. It simplifies the presentation of the code.

**Question:**
* What's the difference between the **ALIAS** in section 3 to the **ALIAS we do here in the JOIN**?

**Answer:**
* In section [Operator section](https://github.com/sshalem/SQL/tree/main/2_Operator_Statements#3) we do ALIAS to a column by adding the key AS
* Here we do [ALIAS](#-) to the tables name w/o the **_AS_** key

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-3

<img src="https://img.shields.io/badge/-2.3. JOIN across Database's %20-yellow" height=30px>

Let's see how we can combine columns form different Database's.</br>
We want to join from 2 different databases.

![image](https://user-images.githubusercontent.com/36256986/163829556-38236937-6462-4765-9e06-f21c6892e536.png)

```sql
SELECT * 
FROM order_items oi
JOIN sql_inventory.products p
	ON oi.product_id = p.product_id;
```

**Question:**
* Why we are doing **_sql_inventory.products_** and not **sql_store.order_items**?

**Answer:**
* It's because the current DB used is **sql_store**.
* since we define it as current DB with command of **USE sql_store;**
That’s why we add it to **sql_inventory.products** because it is **outside the scope** of current DB which is **sql_store**.

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-4

<img src="https://img.shields.io/badge/-2.4. SELF JOINS (INNER)  %20-yellow" height=30px>

In SQL we can **_JOIN a table with itself_**.</br>
Example, let's look at **sql_hr** DB.</br>
It has 2 tables.</br>

![image](https://user-images.githubusercontent.com/36256986/163833827-b4957983-562e-44c6-b532-ae96681dff79.png)

First Let's look at the table of employees and explained how it's possible to make **SELF JOIN**.</br>
We have **employee_id** column and we also have **reports_to** column.

The **reports_to** column is actually the manager .</br>
In the table below all employee's reports to the same manager which is **37270**</br>
The manager itself is an [employee](#-) in that organization.</br>

The managers **employee_id** is **37270** and he reports to **NULL** which means he is the [CEO](#-)

![image](https://user-images.githubusercontent.com/36256986/163834113-96e67237-9e72-49a7-9d94-2d23d2a7638b.png)

### SO let's write a Query to JOIN the table with itself </br>
### So that we will have for each employee its direct manager

```sql
USE sql_hr;

SELECT * 
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id;
```

SELF JOIN table shows there is only one manager in the table.

![image](https://user-images.githubusercontent.com/36256986/163834367-7b4f85e9-a219-41d2-9f6b-720062127d56.png)

This query selects specific fields from the table.

```sql
SELECT 
	e.employee_id, 
	e.first_name AS employee_first_name, 
	m.first_name AS manager_first_name
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id;
```

![image](https://user-images.githubusercontent.com/36256986/163834558-6ba33407-d0ba-4092-83bf-c392c4a151d1.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-5

<img src="https://img.shields.io/badge/-2.5. JOIN more the 2 tables %20-blue" height=40px>

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
