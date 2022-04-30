###### _

<img src="https://img.shields.io/badge/-10. Indexing for high performance %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|     |[Introduction](#Introduction)   |             
|  1  |[Creating Indexes](#Creating_Indexes)   |   
|  2  |[Viewing Indexes](#Viewing_Indexes)   |   
|  3  |[Prefix Indexes](#Prefix_Indexes)   |   




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

###### Viewing_Indexes

<img src="https://img.shields.io/badge/-2. Viewing Indexes  %20-blue" height=40px>

To view the INDEXES we have run both lines (ANALYZE kind of refresh the data so it will be real).

```sql
ANALYZE TABLE customers;
SHOW INDEXES IN customers;
```

following columns shown:
1. [**Key_name**](#-) -  the name of our index
  * **PRIMARY** - this is also called the **Clustered Index**. whenever we add a PK to a table MySql creates automatically an INDEX so we can quickly look up for records by their ID. </br>
  we can see that **PRIMARY** is place at the **customer_id** column.</br>
  Every table can have a max of 1 **Clustered Index**.
  * **secondary_indexes** : **idx_state** and **idx_points** . Technically, whenever we make a **secondary_index** , MySql automatically includes the id or the **PK** column in the **secondary_index**
2. [**Collation**](#-) - represents how data is sorted (A-Ascend, D-Descend)
3. [**Cardinality**](#-) - Represents an estimated number of unique values inthe **INDEX**. we use ANALZYE statement to get Real values.
4.  [**Index_type**](#-) -  BTREE : Binary Tree (Most INDEXES are stored as Binary Tree)

![image](https://user-images.githubusercontent.com/36256986/165847061-3f67adaa-ee1c-43d2-8c97-aafc72aa4b65.png)

### [Example 2] Show order INDEXES



```sql
SHOW INDEXES IN orders;
```

The **secondary_index** shows we have 3 FK columns.
SO Whenever we create a Relationship between 2 tables , MySql automatically creates an INDEX on the Forein Key so we can quickly join our tables.

![image](https://user-images.githubusercontent.com/36256986/165849752-1c00b3ae-b042-4a54-b530-fc6fa55e897a.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Prefix_Indexes

<img src="https://img.shields.io/badge/-3. Prefix Indexes %20-blue" height=40px>

If the column we want to put an INDEX on is a String column (CHAR, VARCHAR, TEXT, BLOB) our INDEX :
1. may consume a lot of space 
2. Won't perfrom well

Smaller INDEXES are better because they can fit in memmory and this :
* makes our search faster

When IDEXING String columns we don't want to include the entire column in the INDEX, we only want to include the first few characters or the [PREFIX](#-) of the column so our INDEX will be smaller.</br>

### [Example](#-)

Let's say we want to create an INDEX on the last_name column in customers table.

```sql
CREATE INDEX idx_lastname ON customers (last_name(20));
```

Question
* Why (last_name(20)) ? 

Answer:
* 20 is the number of characters we want to include in the INDEX.
* This includes only the first 20 caharacters of the INDEX.

THis is how we decide the number of 20.
Let's try a few prefix length and see how many unique values we get.

```sql
SELECT 
    -- The first Character of last_name 
 	  COUNT(DISTINCT LEFT(last_name,1)),
    COUNT(DISTINCT LEFT(last_name,5)) ,
    COUNT(DISTINCT LEFT(last_name,10))
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/166122825-f100da7a-5b2b-4f86-897e-3ac991c96e1c.png)

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
