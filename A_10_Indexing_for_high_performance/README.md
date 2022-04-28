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

Run the following query:

```sql
SELECT customer_id FROM customers WHERE state = 'CA';
```

Let's see how MySql actually runs the above query:




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
