###### _

<img src="https://img.shields.io/badge/-10. Indexing for high performance %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|     |[Introduction](#Introduction)   |             
|  1  |[CREATE DROP SHOW Indexes](#CREATE_DROP_SHOW_Indexes)   |   
|  2  |[Viewing Indexes](#Viewing_Indexes)   |   
|  3  |[Prefix Indexes](#Prefix_Indexes)   |   
|  4  |[Full text Indexes](#Full_text_Indexes)   |   
|  5  |[Composite Indexes](#Composite_Indexes)   |   
|  6  |[Order of Columns in Composite Indexes](#Order_of_Columns_in_Composite_Indexes)   |  
|  7  |[When INDEXES are ignored](#When_INDEXES_are_ignored)   |   
|  8  |[Using Indexes for Sorting](#Using_Indexes_for_Sorting)   |   
|     |8.1							 |[Show_status](#Show_status)   |  

--------------------------------------------------------------------------------------------------

###### Introduction

<img src="https://img.shields.io/badge/-Introduction  %20-blue" height=40px>

[Indexes](#-) speed up our queries dramatically.</br>
[Indexes](#-) are basically data structures , that Database engine use to quickly find data.</br>

https://www.guru99.com/indexing-in-database.html

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

###### CREATE_DROP_SHOW_Indexes

<img src="https://img.shields.io/badge/-1. CREATE DROP SHOW Indexes %20-blue" height=40px>

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

### [CREATE INDEX and EXPLAIN](#-)

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

### [Command to SHOW INDEXES](#-)

```sql
SHOW INDEXES IN customers;
```

### [Command to DROP INDEXES](#-)

```sql
DROP INDEX idx_points ON customers;
DROP INDEX idx_state ON customers;
SHOW INDEXES IN customers;
```


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

THis is how we decide the number of 20. </br>
Let's try a few prefix length and see how many unique values we get.</br>
Our goal here, is to maximize the number of unique values is our INDEX.</br>
So we try different length number.

```sql
SELECT 
    -- The first Character of last_name 
 	  COUNT(DISTINCT LEFT(last_name,1)),
    -- The first 5 Character of last_name 
    COUNT(DISTINCT LEFT(last_name,5)) ,
    -- The first 10 Character of last_name 
    COUNT(DISTINCT LEFT(last_name,10))
FROM customers;
```

5 has 966 unique values.
10 has 996 unique values.

![image](https://user-images.githubusercontent.com/36256986/166123337-394a4349-6b8c-4a9f-a106-5b7444a18e7f.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Full_text_Indexes

<img src="https://img.shields.io/badge/-4. Full_text_Indexes %20-blue" height=40px>

We use [FULL TEXT INDEX](#-) to build fast and felxible apps in our search engines.
A full-text index in MySQL is an index of type FULLTEXT . Full-text indexes can be used only with InnoDB or MyISAM tables, and can be created only for CHAR , VARCHAR , or TEXT columns. </br>

For the lecture ,Download the new script ```create-db-blog.sql``` and run it.</br>

Let's say we're gong to build a blog web site and give our users the abilit to search for blog posts.</br>
Let's say someone searches for 'react redux' , how we can find posts that are about 'react redux'?</br>

Create FULL TEXT INDEX

```sql
CREATE FULLTEXT INDEX idx_title_body ON posts (title, body);
```


### [First way](#-)

```sql
SELECT * 
FROM posts
WHERE 
	title LIKE '%react%' OR title LIKE '%Redux%'
    OR body LIKE '%react%' OR body LIKE '%redux%';
```

This gives following result:

![image](https://user-images.githubusercontent.com/36256986/166130794-7573589c-725c-4a00-987d-5abc6080d471.png)

### [Second way](#-)

By creating a [FULL TEXT INDEX](#-)

In this SQL query the words 'react redux' can be together or be seperated by words between them.
```sql
SELECT *
FROM posts
WHERE MATCH(title, body) AGAINST('react redux');

EXPLAIN SELECT * FROM posts WHERE MATCH(title, body) AGAINST('react redux');
```

Gives same result as in Fisrt way above.

![image](https://user-images.githubusercontent.com/36256986/166130794-7573589c-725c-4a00-987d-5abc6080d471.png)

```sql
EXPLAIN SELECT * FROM posts WHERE MATCH(title, body) AGAINST('react redux');
```

![image](https://user-images.githubusercontent.com/36256986/166131377-5135c77c-4087-47f0-8f20-417d67d6f5a3.png)

### [Third way with **_RELEVENCY SCORE_** in default mode](#-)

One of the benfits they include relevence score. So based on anumber of factors ,MySql calculates the relevency score for each row ,that calculates the search phrase. </br>
The relevency score is afloting point number between 0 to 1.</br>
0 - means no relevence

Full Text search has 2 modes.
1. default mode - natural language mode (which is default mode) , this is what we used in the example above.
2. Boolean mode - with this mode we can include/exclude certain words just like hw we use google.

```sql
SELECT * , MATCH(title, body) AGAINST('react redux')
FROM posts
WHERE MATCH(title, body) AGAINST('react redux');
```

We have 2 columns added , date published, Relevency_score.</br>
The results are sorted by relevency score in descending order.</br>
This isvery powerful , just like search engines like google. 

![image](https://user-images.githubusercontent.com/36256986/166131066-595ab87e-f2ca-43ca-ab9e-b4f801b4c826.png)


### [Third way with **_RELEVENCY SCORE_** in BOOLEAN mode](#-)

```sql
SELECT * , MATCH(title, body) AGAINST('react redux')
FROM posts
WHERE MATCH(title, body) AGAINST('react -redux' IN BOOLEAN MODE);
```

```sql
SELECT * , MATCH(title, body) AGAINST('react redux')
FROM posts
WHERE MATCH(title, body) AGAINST('react -redux +form' IN BOOLEAN MODE);
```

```sql
SELECT * , MATCH(title, body) AGAINST('react redux')
FROM posts
WHERE MATCH(title, body) AGAINST('"handling a form"' IN BOOLEAN MODE);
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Composite_Indexes

<img src="https://img.shields.io/badge/-5. Composite_Indexes %20-blue" height=40px>

Let's look at the INDEXES in customers table.

```sql
SHOW INDEXES IN customers;
```

We have on Primary (Cluster INDEX) INDEX + 3 secondary INDEXES.

![image](https://user-images.githubusercontent.com/36256986/166142090-4b923013-096d-4dca-a37b-997828ebf2ba.png)

Let's say we want to look for customers located in CA who have more than a 1000 points.</br>
So let's write the Query for it.

```sql
EXPLAIN SELECT customer_id FROM customers WHERE state = 'CA' AND points > 1000;
```

MySql take the **idx_state** column, so no matter how many INDEXSES I have , MySql will take the maximum of 1 INDEX.</br>
Number of [**ROWS is 112**](#-). this means it scans 112 times the table for points. 

![image](https://user-images.githubusercontent.com/36256986/166142273-30455ab0-0f72-40d1-bf29-c67e75d1eeba.png)

### [Composite INDEX](#-)

with the composite INDEX we can INDEX multiple columns. </br>
So we can make a Copmposite INDEX of state & points.</br>
Let's create new INDEX called **idx_state_points**

```sql
CREATE INDEX idx_state_points ON customers (state,points);
EXPLAIN SELECT customer_id FROM customers WHERE state = 'CA' AND points > 1000;
```

Number of [**ROWS is 58**](#-). 

![image](https://user-images.githubusercontent.com/36256986/166142596-bda86ccd-d64f-4bdb-9bf1-38b655bcc61d.png)

* Most of the time we should use composite INDEXES because a query can have multiple filters.
* INDEXES can help us store data faster, so if we have multiple columns in an INDEX , we can also speed up **SORTING** of our data
* Need to know ,the more INDEXES we have the slower the write operations are going to be.
* MySql Automativally includes the PRIMARY key of the table , in each secondary INDEX. 
* If we have a lot of Single column INDEXES ,they are going to waste a lot of space. and That's why it's better to [**Composite INDEXES**](#-).

[How many columns should we include in our INDEXES?](#-) </br>
In MySql an INDEX can have a maximum of 16 columns. (4 to 6 columns perform well But don't take it as  a rule or best practice) .

### [DROP unnecesseray indexes for better perefromance](#-)

```sql
-- Lets' drop the unnecesseray indexes
DROP INDEX idx_points ON customers;
DROP INDEX idx_state ON customers;

SHOW INDEXES IN customers;
```

![image](https://user-images.githubusercontent.com/36256986/166158420-bf3d43ca-3e31-46a0-8b79-42bcb7f413a3.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Order_of_Columns_in_Composite_Indexes

<img src="https://img.shields.io/badge/-6. Order_of_Columns_in_Composite_Indexes %20-blue" height=40px>

* Put the most frequently columns used first
* Put the columns with a higher CARDINALITY first(CARDINALITY  means The number of unique values in the INDEX) 

```sql
SHOW INDEXES IN cusotmers;
```

The CARDINLITY of Primary key is 1010. (So 1010 unique values)

![image](https://user-images.githubusercontent.com/36256986/166158642-91d84e41-5166-4ca7-81b0-c57d13014df1.png)

### [Case study](#-)
* If we have for example a table with column of gender (which have 2 options male/female, The Cardinality will be 2) and a million row. So in our Composite INDEX , if we put our gender first , this column can narrow down our searches from 1 million to 500K. 
* Now, what if we put our state column first. In our customers table we have 48 unique states. Assume we have 1 million records in the table an even distibution of customers across states , we are going to have 1 million / 48 ~ 20K Roughly 20K customers in each state). SO if we put our state column first this can nrrow down our searches to fewer records.

* So , as a basic RULE , better put the columns with higher carinality first , BUT don't take this as a hard and FAST rule . This is just a starting point, you should always take your query and the date time into account.

### [Example to show that NOT always the first column should be with higher Cardinallity](#-)

We have the following query.

[Question](#-)
* which columns should come first in our INDEX?

```sql
SELECT customer_id
FROM customers 
WHERE state = 'CA' AND last_name LIKE 'A%';
```

[Answer](#-)
* Lets look at the cardinality of these columns.

```sql
SELECT 
	COUNT(DISTINCT state) AS states,
	COUNT(DISTINCT last_name) AS last_names
FROM customers;
```

states has cardinality of 48, last_names has 996.

![image](https://user-images.githubusercontent.com/36256986/166163910-432d3fe3-5c32-4fbc-a27c-30dabab34917.png)

Let's create 2 INDEXES as follows:

```sql
CREATE INDEX idx_lastname_state ON customers(last_name, state);
CREATE INDEX idx_state_lastname ON customers(state, last_name);
```

Now lets run the following SQL with INDEX of **idx_lastname_state**:

```sql
EXPLAIN SELECT 
	ROW_NUMBER() OVER() AS Id,
	customer_id
FROM customers 
USE INDEX(idx_lastname_state)
WHERE state = 'CA' AND last_name LIKE 'A%';
```

When using INDEX of idx_lastname_state we get 40 rows:

![image](https://user-images.githubusercontent.com/36256986/166164421-c18480a7-a264-4a16-9ace-3753d744f9ab.png)

Lets use the INDEX of **idx_state_lastname**

```sql
EXPLAIN SELECT 
	ROW_NUMBER() OVER() AS Id,
	customer_id
FROM customers 
USE INDEX(idx_state_lastname)
WHERE state = 'CA' AND last_name LIKE 'A%';
```

When using INDEX of idx_lastname_state we get 7 rows:

![image](https://user-images.githubusercontent.com/36256986/166164475-26ed77f2-b0a9-4e4b-b241-c2b08b846bc5.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### When_INDEXES_are_ignored

<img src="https://img.shields.io/badge/-7. When INDEXES are ignored  %20-blue" height=40px>

There are situations where we have an IDEX but we still expirience performance problems.
Let's look at some of the common scenarios.

### [Example 1](#-)

Lets EXPLAIN the following Query:

```sql
EXPLAIN SELECT customer_id FROM customers
WHERE state = 'CA' OR points > 1000;
```

type - index </br>
key  - idx_state_points </br>

It looks like we have a full table sacn (because row is 1010) BUT actually we don't. </br>
Because the value of the **_type = index_** which means we have a full index scan. </br>
this is faster than a table scan because it doesn't envolve reading every record from the disk. Having said that we still have to sacn 1010 rows.</br>

![image](https://user-images.githubusercontent.com/36256986/166164918-ac768c1a-b8a1-4e78-93ac-29abdb6a7fa9.png)

SO how can we optimze this query further? </br>
This is one of the situations where we have to re-write our query to utilize the INDEXES in the best possible way.</br>
In this case we're going to chop up this query into two smaller queries. </br>
First, we're going to select  allcustomers located in the state of CA , the we're going to UNION that with another query that picks customers that have more than a 1000 points.

We create a new INDEX idx_points as well for better performance.

```sql
CREATE INDEX idx_points ON customers(points);

EXPLAIN 
    SELECT customer_id FROM customers
    WHERE state = 'CA' 
    UNION
    SELECT customer_id FROM customers
    WHERE points > 1000;
```

The EXPLAIN gives :

for idx_state_points 112 rows  </br>
for idx_points 529 rows  </br>
together it will search in 641 rows  </br>

![image](https://user-images.githubusercontent.com/36256986/166165365-180bb28f-4151-465b-8b84-47da0ca05050.png)

### [Example 2](#-)

Let's EXPLAIN the following query:

```sql
EXPLAIN 
	SELECT customer_id FROM customers
	WHERE points + 10 > 2010;
```

type - index   </br>
key  - idx_points  </br>
rows - 1010  </br>

![image](https://user-images.githubusercontent.com/36256986/166165472-1fb4f20e-1f17-4978-81b4-cbd6968801d8.png)

* What is the reason we have a full scan?
* That is because of the Expression **points + 10 > 2010**

to improve it lets query like this:

```sql
EXPLAIN 
	SELECT customer_id FROM customers
	WHERE points > 2000;
```

Now we get 4 rows .

![image](https://user-images.githubusercontent.com/36256986/166165588-948943d9-8b4e-4006-b5de-744d94343c6e.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)


--------------------------------------------------------------------------------------------------

###### Using_Indexes_for_Sorting

<img src="https://img.shields.io/badge/-8. Using Indexes for Sorting  %20-blue" height=40px>

So far we used INDEXES for filtering data. </br>
We can also use INDEXES for sorting data. </br>

These are the INDEXES we have now:

```sql
SHOW INDEXES IN customers;
```

![image](https://user-images.githubusercontent.com/36256986/166165876-1b4c131d-2239-4df5-9037-4047c9e62e69.png)

### [Write Query to sort customers by their state](#-)

```sql
EXPLAIN 
	SELECT customer_id FROM customers ORDER BY state;
```

type  - index </br>
key   - idx_state_points </br>
rows  - 1010  </br>
extra - Using index

![image](https://user-images.githubusercontent.com/36256986/166166290-45fe5d70-2f01-42a0-b4b1-31feb39b6ab0.png)

Let's see what happens if we SORT by different column that is not in our INDEX:

```sql
EXPLAIN 
    SELECT customer_id 
    FROM customers 
    ORDER BY first_name;
```

type  - all (Full table scan) </br>
key   - null </br>
rows  - 1010  </br>
extra - Using filesort (filesort - is the name of the algorithm that MySql uses to sort data in a table) </br>

filesort - is very expensive operation.

![image](https://user-images.githubusercontent.com/36256986/166166396-4d240846-3ba2-4f32-9b8b-dd7ff0ca7070.png)

Lets see how cost it's worth:

```sql
SHOW STATUS LIKE 'last_query_cost';
```

![image](https://user-images.githubusercontent.com/36256986/166166684-1324c643-6f09-4559-9b67-ee3f923195f3.png)

Let's sort with column that is our INDEX:

```sql
EXPLAIN 
    SELECT customer_id FROM customers 
    ORDER BY state;

SHOW STATUS LIKE 'last_query_cost';	
```

![image](https://user-images.githubusercontent.com/36256986/166166730-fc29a2d5-9856-4fb5-882a-a00108d558a2.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Show_status

<img src="https://img.shields.io/badge/-8.1. Show Status %20-blue" height=40px>

the SHOW STATUS statement , to look at the server variables.

```sql
SHOW STATUS;
```

These are the variables used by MySql server. See usage in section 8.

![image](https://user-images.githubusercontent.com/36256986/166166603-4edf4426-5968-45eb-86ac-ed56ee04a845.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
