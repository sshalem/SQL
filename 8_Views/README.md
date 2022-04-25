###### _

<img src="https://img.shields.io/badge/-8. Views %20-blue" height=60px>

|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[What are VIEWS](#1)   |             
|  2  |[Creating Views](#2)   |
|  3  |[3](#3)   | 
|  4  |[4](#4)   | 
|  5  |[5](#5)   | 
|  6  |[6](#6)   | 
|  7  |[7](#7)   | 
|  8  |[8](#8)   | 


--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-1. What are VIEWS  %20-blue" height=40px>

[Question](#-)
* What are VIEWS?

[Answer](#-)
* VIEW are saved Querirs or SubQuerirs 

We can save Queries in a [VIEW](#-) , and reuse them later .this will simplyfies our SELECT statement.

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. Creating Views %20-blue" height=40px>

Let's see how we create a VIEW.</br>

* [First](#-): Let's create a Query that produces the result below. </br>
This is a very useful Query, if in the future we might have alot of queries that will be based on this query, </br>
We can save it in a view  and reuse that view in many places.

```sql
SELECT 
	  c.client_id,
    c.name,
    SUM(invoice_total) AS total_sales
FROM clients c
JOIN invoices i USING(client_id)
GROUP BY client_id, name;
```

![image](https://user-images.githubusercontent.com/36256986/165045515-c339c23e-ba18-4000-8ea6-c60720b817dd.png)

* [Second](#-) Let's create the view.</br>
I add the following line ```CREATE VIEW sales_by_client AS``` then execute the code.
After Execution MySql create a VIEW object of **_sales_by_client_**.

```sql
CREATE VIEW sales_by_client AS
SELECT 
	  c.client_id,
    c.name,
    SUM(invoice_total) AS total_sales
FROM clients c
JOIN invoices i USING(client_id)
GROUP BY client_id, name;
```

Refresh the DB , Now we have a VIEW object of **_sales_by_client_**.

![image](https://user-images.githubusercontent.com/36256986/165046680-7adf2eba-cc51-40a8-9aeb-cbdbf234d261.png)



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
