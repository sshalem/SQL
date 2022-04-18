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
|     |2.6				 |[JOIN from table with CK](#2-6)   |
|  3  |[OUTER JOIN](#3)   | 
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

The **_INNER JOIN_** keyword selects records that have **_matching values in both tables_**.
![image](https://user-images.githubusercontent.com/36256986/163840831-2644071b-3209-4229-9ac6-cb9f0f4ac1b5.png)

(see the difference in LFET/RIGHT JOIN)

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
Example, let's look at **_sql_hr_** DB.</br>
It has 2 tables.</br>

![image](https://user-images.githubusercontent.com/36256986/163833827-b4957983-562e-44c6-b532-ae96681dff79.png)

First Let's look at the table of employees and explained how it's possible to make **_SELF JOIN_**.</br>
We have **_employee_id_** column and we also have **_reports_to_** column.

The **_reports_to_** column is actually the manager .</br>
In the table below all employee's reports to the same manager which is **_37270_**</br>
The manager itself is an [_employee_](#-) in that organization.</br>

The managers **_employee_id_** is **_37270_** and he reports to **_NULL_** which means he is the [_CEO_](#-)

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

<img src="https://img.shields.io/badge/-2.5. JOIN more the 2 tables %20-yellow" height=30px>

Let's look at the **_orders , customers & order_statuses_** tables from **_sql_store_** DB.

### [orders](#-)
![image](https://user-images.githubusercontent.com/36256986/163835157-604e636b-9e28-42c0-a06e-f123b191c653.png)

### [customers](#-)
![image](https://user-images.githubusercontent.com/36256986/163836832-6d8756e1-b601-4633-acc8-facf99eb8ff9.png)

### [order_statuses](#-)
![image](https://user-images.githubusercontent.com/36256986/163836884-63f1b202-7c7a-4efa-91c7-5002800b4cf3.png)

**_orders_** table  has the following keys:
1. order_id - [PK](#-)
2. customer_id - [FK](#-)
3. status - [FK](#-)
4. shipper_id - [FK](#-)

Let's run a query to join data from **_3 tables_**:

```sql
SELECT 
	o.order_id,
	o.order_date,
	c.first_name,
	c.last_name,
	os.name AS status
FROM orders o 
	JOIN customers c
		ON c.customer_id = o.customer_id
	JOIN order_statuses os
		ON o.status = os.order_status_id;
```

![image](https://user-images.githubusercontent.com/36256986/163836015-08b84978-e7d0-40ea-948f-ad30c1f7ccaa.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-6

<img src="https://img.shields.io/badge/-2.6. JOIN from table with CK %20-blue" height=40px>

Let's see how to JOIN a table that has a **_CK_**. </br>
The **_order_items_** table has a **_CK_** . </br>
The CK is composite of 2 FK wich are:
1) order_id
2) product_id

![image](https://user-images.githubusercontent.com/36256986/163837872-b7b1be50-e8d9-4dd3-b6e9-f63183f6d357.png)

Let's look at the **_order_item_notes_** table:

(**_note_id_** is the PK in this table)

![image](https://user-images.githubusercontent.com/36256986/163838561-12f43ddb-f4bf-4893-8370-522fc4fbecda.png)

This query uses the compound key of the table 

```sql
SELECT *
FROM order_items oi
	JOIN order_item_notes oin
		ON oi.order_id = oin.order_id
		AND oi.product_id = oin.product_id;
```

![image](https://user-images.githubusercontent.com/36256986/163838859-8becae00-8c0e-40e6-b584-65af5c0e2a2e.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-3. OUTER JOIN %20-blue" height=40px>

Let’s first understand what we get from INNER JOIN.

Let's look at the tables of :

	1. customers
	2. orders

### [Customers](#-)
![image](https://user-images.githubusercontent.com/36256986/163839542-debb4ad5-137a-4750-a5a3-69bd673f3543.png)

### [Orders](#-)

We can see in this table that [**some of the customers don't have orders**](#-).

![image](https://user-images.githubusercontent.com/36256986/163839555-1a8f4526-ce8b-46aa-bfdb-b1004e64bf44.png)

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
