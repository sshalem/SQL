###### _

<img src="https://img.shields.io/badge/-3_Operator Statements%20-blue" height=60px>

|     |  Subject           |             | 
|:---:|:------------------------------|:------| 
|  1  |[USE](#1)   |    |
|  2  |[SELECT](#2)   |     |
|     |            |[SELECT with Arithmetic *  /  +  -  %](#2-1) |
|  3  |[ALIAS](#3)   |           |
|  4  |[DISTINCT](#-)   |        |
|  5  |[WHERE](#-)   |     |
|  6  |[Logical Operators AND, OR, NOT](#-)   |     |
|  7  |[IN](#-)   |    |
|  8  |[BETWEEN](#-)   |     |
|  9  |[LIKE](#-)   |      |
|  10  |[REGEX](#-)   |    |
|  11  |[IS NULL](#-)   |   |
|  12  |[ORDER BY](#-)   |    |
|  13  |[LIMIT](#-)   |    |


--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-1. USE %20-blue" height=40px>

The keyword USE chooses the DB we want to work with

Example:

```sql
USE sql_store;
```

This command will highlight the DB we chose

![image](https://user-images.githubusercontent.com/36256986/163691895-9b96ef16-b5ba-4a3f-b2b5-10331231e681.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. SELECT %20-blue" height=40px>

Let's take A look at customers table.

```sql
SELECT * FROM customers;
```

Will give the same table as we see below.

![image](https://user-images.githubusercontent.com/36256986/163691948-e5f97405-bd62-4717-ac22-5f97ea4deb72.png)

Following query will give a table with custmer_id field only.

```sql
SELECT customer_id 
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163691986-bd647e40-d97f-4006-a4d1-81a57013c409.png)

The query will give a table with fields of : custmer_id , last_name,& city.

```sql
SELECT customer_id, last_name, city 
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163692013-16c4d403-0501-4989-8469-e076b8a985c1.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2-1

<img src="https://img.shields.io/badge/-2.1. [SELECT with Arithmetic *  /  +  -  %](#-) % %20-blue" height=40px>

```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-3. ALIAS %20-blue" height=40px>

```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------
