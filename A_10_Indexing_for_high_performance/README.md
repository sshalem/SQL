###### _

<img src="https://img.shields.io/badge/-10. Indexing for high performance %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|     |[Introduction](#Introduction)   |             
|  1  |[Creating Indexes](#Creating_Indexes)   |             




--------------------------------------------------------------------------------------------------

###### Introduction

<img src="https://img.shields.io/badge/-Introduction  %20-blue" height=40px>

[Indexes](#-) speed up our queries dramatically.</br>
[Indexes](#-) are basically data structures , that Database engine use to quickly find data.</br>

### Cost of [Indexes](#-)

1. [Increase DB](#-) - They increase the size of our DB, because they have to permenently stored next to our tables.
2. [Slow down the writes](#-) - every time we ADD, UPDATE, DELETE a record , MySql has to update the corresponding [INDEXES](#-) . this will impact the perfromance of our right operations.

We should reserve [Indexes](#-) for performance critical queries. </br>
One of the common mistakes developers do is that they add [Indexes](#-) at the time of designing thier tables.</br>
We don't create [Indexes](#-) based on our tables.</br>
We create [Indexes](#-) based on our queries.</br>

Because the whole point of [Indexes](#-) is to speed up a Slow Query.

* Internally, [Indexes](#-) are often stored as BIANTRY tree

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
--------------------------------------------------------------------------------------------------

###### Creating_Indexes

<img src="https://img.shields.io/badge/-1. Creating Indexes %20-blue" height=40px>

### Before starting , run the sql script [**_load_1000_customers.sql_**.](#-)

When doing INDEX, we cannot use ``SELECT *``` we must specify the columns name. </br>
Run the following query:

```sql
SELECT customer_id FROM customers WHERE state = 'CA';
```

Let's see how MySql actually runs the above query. </br>
Run the following QUery (new keyword EXPLAIN is used)

```sql
EXPLAIN SELECT customer_id FROM customers WHERE state = 'CA';
```
we will the see use of each column later in the section, but for now pay attention to our :
1. type
2. rows

When we see a **type = all** , MySql will do a full table scan , which means it's going to read every single record in the table.</br>
In the **rows** column , we see the number that it scanned **rows=1010**.

![image](https://user-images.githubusercontent.com/36256986/165841137-a90aacdc-3529-4af4-83e9-6e5d30ec5d06.png)

Because we don't have an **_INDEX_** on our table , MySql will have to scan every single record in the table. (Imgaine we have millions of records).
This is where we add **_INDEX_** to our table.</br>

SO we will add an **_INDEX_** on our **_state_** column to which speed up the query.

```sql
CREATE INDEX idx_state ON customers (state);
EXPLAIN SELECT customer_id FROM customers WHERE state = 'CA';
```

We can see following changes : </br>
* **type = ref** 
* **possible_keys=idx_state**
* **key=idx_state**
* **key_len=8**
* [**rows=112**](#-)
* **filtered=100**
* **extra=Using index**

![image](https://user-images.githubusercontent.com/36256986/165843556-62a13144-de83-41bf-874b-7c37be201553.png)

### [Exercise](#-)

Write a query to find customers with more than 1000 points.

```sql
CREATE INDEX idx_points ON customers (points);
EXPLAIN SELECT customer_id FROM customers WHERE points > 1000;
SELECT * FROM customers WHERE points > 1000;
```

We can see following changes : </br>
* **type = range** 
* **possible_keys=idx_points**
* **key=idx_points**
* **key_len=4**
* [**rows=529**](#-)
* 
![image](https://user-images.githubusercontent.com/36256986/165845771-8c91dac8-d568-42f0-8df0-2ef55eef073e.png)

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
