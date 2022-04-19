###### _

<img src="https://img.shields.io/badge/-5. Summerizing Data %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[Aggregate Functions](#1)   |[MAX() MIN() SUM() AVG() COUNT()](#-)    |
|  2  |[GROUP BY clasue](#2)   		 | 
|     |3.1				 |[OUTER JOIN syntax with LEFT/RIGHT](#3-1)   | 
|     |3.2				 |[LEFT JOIN best practice](#3-2)   | 
|     |3.3				 |[LEFT JOIN](#3-3)   | 
|     |3.4				 |[RIGHT JOIN](#3-4)   | 
|     |3.5				 |[OUTER JOIN more than 2 tables](#3-5)   | 
|     |3.6 				 |[SELF OUTER JOIN](#3-6)   |
|  4  |[USING CLAUSE](#4)   |  
|     |4.1				 |[USING clause on CK](#4-1)   |  
|  5  |[NATURAL JOIN](#5)   |  
|  6  |[CROSS JOIN](#6)   |  
|  7  |[UNION](#7)   | 
|     |7.1				  |[UNION same table](#7-1)   | 
|     |7.2				  |[UNION different table](#7-2)   | 



--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-1. Aggregate Functions %20-blue" height=40px>

These are useful Aggregate functions:
* MAX()
* MIN()
* AVG()
* SUM()
* COUNT()

In this section I will use for the demo the DB of [sql_invoicing](#-) from table [invoices](#-)

![image](https://user-images.githubusercontent.com/36256986/164080490-1e96f6b3-fdcb-43b3-adbf-4fea1278f318.png)

We can use Aggregate functions on:
1. Numeric values
2. String
3. Dates
4. They [only](#-) operate on [Non Null](#-) values
5. By Default , all the functions take duplicate values


### [example 1](#-)

```sql
SELECT COUNT(*) AS total_records FROM invoices;
```

![image](https://user-images.githubusercontent.com/36256986/164083532-48fed5d5-ac0e-4233-b580-d0007286c55e.png)


### [example 2](#-)

I use Aggregate funtions on [Numeric values](#-):

```sql
SELECT 
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total) AS total,
    COUNT(invoice_total) AS number_of_invoices    
FROM invoices;
```

![image](https://user-images.githubusercontent.com/36256986/164081022-34b8e487-d5d5-4631-9f91-763585cfe36f.png)

### [example 3](#-)

In this example I will show the use of Numeric values & Date. </br>
The query count 2 things:
1. MAX(payment_date)  - Date value
2. COUNT(invoice_total)   - Numeric value
3. COUNT(payment_date)  - Numeric value

```sql
SELECT 
    MAX(payment_date) AS highest_payment_date,
    COUNT(invoice_total) AS number_of_invoices,
    COUNT(payment_date) AS count_of_payments
FROM invoices;
```

We can see we got COUNT(payment_date) is 7 because the rest are NULL values, because Aggregate values work only on NON NULL values .

![image](https://user-images.githubusercontent.com/36256986/164082703-9dbeb9ec-8fba-4898-b257-292269dd32c5.png)

### [example 4](#-)

```sql
SELECT 
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(*) AS total_records   
FROM invoices
WHERE invoice_date > '2019-07-01';
```

we added a filter of **invoice_date > '2019-07-01'** thus we got only 7 records. <br>
In the **SUM(invoice_total * 1.1)** fuction: 
* first calc  **(invoice_total * 1.1)**  
* then makes the **SUM()**

![image](https://user-images.githubusercontent.com/36256986/164084240-aa5625bb-6c3c-4f80-ba84-c1bc7cab397c.png)

### [example 5](#-)

Since by default all functions take duplicate vlaues we can use the DISTINCT clause.</br>
This query below will give duplicate values since we have same client_id in the [invoices](#-) 

```sql
SELECT 
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(DISTINCT client_id) AS total_records   
FROM invoices
WHERE invoice_date > '2019-07-01';
```

We have 7 records since there are duplications.

![image](https://user-images.githubusercontent.com/36256986/164086230-9f944c34-76e6-4c12-abba-f6ea3ab39630.png)

Lets run same query , but now , Iadd the DISTINCT clause:

```sql
SELECT 
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(DISTINCT client_id) AS total_records   
FROM invoices
WHERE invoice_date > '2019-07-01';
```

Now we have 3 records and not 7.

![image](https://user-images.githubusercontent.com/36256986/164086053-65ce2838-8516-45b8-93ef-072066db9fd6.png)


### [example 6](#-)

Write a Query that gives the following result:

![image](https://user-images.githubusercontent.com/36256986/164089100-2c29e697-3cfd-4e41-a599-98699206f52b.png)

```sql
SELECT 
    'First half of 2019' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payment,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date 
	BETWEEN '2019-01-01' AND '2019-06-30'
UNION
SELECT 
    'Second half of 2019' AS date_range,   
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payment,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date 
	BETWEEN '2019-07-01' AND '2019-12-31'
UNION
SELECT 
    'Total' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payment,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date 
	BETWEEN '2019-01-01' AND '2019-12-31';
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. GROUP BY clasue %20-blue" height=40px>

So far we saw we can have the invoice_total of the table. 

```sql
SELECT SUM(invoice_total) FROM invoices;
```

![image](https://user-images.githubusercontent.com/36256986/164090238-4e67e11c-abde-4315-a89a-2f76737462f0.png)

[Question](#-)
* What if we want to see the total sales per client.

[Answer](#-)
* That is where we need to **_GROUP BY_** data, by 1 or more columns.

### [example 1](#-) [**_GROUP BY_** single column](#-)

This query will show the **SUM** of each **client_id** (it is [GROUP BY](#-) **client_id**)

```sql
SELECT 
	SUM(invoice_total) 
FROM invoices
GROUP BY client_id;
```

![image](https://user-images.githubusercontent.com/36256986/164091067-01549fe7-e2a2-45c1-8a72-9adca09e5503.png)

Lets add columns of client_id and number , and **ORDER BY** **_DESC_** order:

```sql
SELECT 
    client_id,
    number,
    SUM(invoice_total) AS total_sales
FROM invoices
WHERE invoice_date >= '2019-07-01'
GROUP BY client_id
ORDER BY total_sales DESC;
```

![image](https://user-images.githubusercontent.com/36256986/164092730-8d0ec509-1b2c-4a96-af3d-c3760a060f8d.png)

### [example 2](#-) [**_GROUP BY_** multiple columns](#-)

```sql
SELECT 
    state,
    city,    
    SUM(invoice_total) AS total_sales
FROM invoices i
JOIN clients USING(client_id)
GROUP BY state, city;
```

we don't have multiple Cities for each state , so check for beter example to understand.

![image](https://user-images.githubusercontent.com/36256986/164094365-23aca5ff-f6f2-4128-aa0d-f8eb2470bc49.png)

### [example 3](#-) [**_GROUP BY_** Excersize](#-)

WE have a query that generates this report:


Write a query to generate the report.

```sql

```

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

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
