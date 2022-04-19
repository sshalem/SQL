###### _

<img src="https://img.shields.io/badge/-5. Summerizing Data %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[Aggregate Functions](#1)   |		     |
|     |1.1               |[MAX()](#1-1)       |
|     |1.2				 |[MIN()](#1-2)    |
|     |1.3				 |[AVG()](#1-3)   |
|     |1.4				 |[SUM()](#1-4)   | 
|     |1.5				 |[COUNT()](#1-5)   | 
|  2  |[OUTER JOIN](#3)   		 | 
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

In this section I will use for the demo the DB of [sql_invoicing](#-)

![image](https://user-images.githubusercontent.com/36256986/164080490-1e96f6b3-fdcb-43b3-adbf-4fea1278f318.png)

We can use Aggregate functions on:
1. Numeric values
2. String
3. Dates
4. They [only](#-) operate on [Non Null](#-) values

### example 1:

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

### example 2

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



[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. INNER JOIN (or Just JOIN) %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)


