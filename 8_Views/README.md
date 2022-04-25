###### _

<img src="https://img.shields.io/badge/-8. Views %20-blue" height=60px>

|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[What are VIEWS](#1)   |             
|  2  |[Creating VIEWS](#2)   |
|  3  |[Using VIEWS](#3)   | 
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

[VIEW](#-) behaves like a [virtual table](#-)  , **_BUT_** , </br> 
VIEW don't store DATA. Our DATA is actually sotred in our tables .  </br> 
That is why they are called [VIEW's](#-)

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

###### 3

<img src="https://img.shields.io/badge/-3. Using VIEWS  %20-blue" height=40px>

* Let's see how we can use VIEW's.

### 1. use as a table and apply filters

```sql
SELECT * 
FROM sales_by_client
WHERE total_sales > 500;
```

![image](https://user-images.githubusercontent.com/36256986/165048021-84ebd038-6b3f-4c8f-a563-13ba5401440d.png)

### 2. we can JOIN the VIEW 

```sql
SELECT * 
FROM sales_by_client
JOIN clients USING(client_id);
```

![image](https://user-images.githubusercontent.com/36256986/165048099-3b54c739-9534-4b0e-a6f6-ecde70c086fb.png)

### [**Exercise**](#-) 

- Create a view to see the balance for each client
- VIEW Name: clients_balance
- VIEW should have these columns : client_id, name, balance(payment_total - invoice_total)

### [**Solution**](#-) 

Let's make it in 3 steps.

#### [Step1](#-)

```sql
SELECT 
     client_id,
     name,
     invoice_total - payment_total AS balance
FROM clients c
JOIN invoices i USING(client_id);
```

Query creates following table:

![image](https://user-images.githubusercontent.com/36256986/165052501-4176312a-be7b-459a-9bc8-1019ce21b581.png)

#### [Step2](#-)

Let's add aggregation Function of **SUM(invoice_total - payment_total)** and **GROUP BY client_id, name**

```sql
SELECT 
     client_id,
     name,
     SUM(invoice_total - payment_total) AS balance
FROM clients c
JOIN invoices i USING(client_id)
GROUP BY client_id, name;
```

Query creates following table:

![image](https://user-images.githubusercontent.com/36256986/165052910-f1cf09af-bffe-4dd1-85e0-3933bc9bb996.png)

#### [Step3](#-)

Let's create a [VIEW](#-) :

```sql
CREATE VIEW clients_balance AS
SELECT 
     client_id,
     name,
     SUM(invoice_total - payment_total) AS balance
FROM clients c
JOIN invoices i USING(client_id)
GROUP BY client_id, name;
```

![image](https://user-images.githubusercontent.com/36256986/165053186-f54b98a6-126b-417a-91e8-75bc0ebb8ceb.png)

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
