###### _

<img src="https://img.shields.io/badge/-3_Operator Statements%20-blue" height=60px>

|     |  Subject           |             | 
|:---:|:------------------------------|:------| 
|  1  |[USE](#1)   |    |
|  2  |[SELECT](#2)   |     |
|     |2.1.            |[SELECT with Arithmetic *  /  +  -  %](#2-1) |
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

<img src="https://img.shields.io/badge/-2.1. SELECT with Arithmetic %20-blue" height=40px>

This section we will see the use of **SELECT** with **Arithmetic**          

We can use the following : 
* Add : [+](#-)
* Sub:  [-](#-) 
* Div : [/](#-) 
* Mult: [* ](#-) 
* Module: [%](#-) (Residual)

Let's take a look only on the following 3 columns:

```sql
SELECT 
  last_name, 
  first_name, 
  points 
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716276-549fe8d1-71ac-4e0b-ba79-e5ab8dbc1951.png)

Let's say we want to add to a column  of pints the value of 10.</br>
The Query below created new column with modified value.

```sql
SELECT 
  last_name, 
  first_name, 
  points, 
  points+10
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716327-0b97e964-93fd-4c42-801c-276957cba480.png)

Let's say we want to add to a column  of points the value of 10 and Multiply it by 100.</br>
The Query below created new column with modified value.

```sql
SELECT 
    last_name, 
    first_name, 
    points , 
    (points+10 ) * 100
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716434-83d99e04-138a-4cf7-a2f1-e495af8bbc69.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-3. ALIAS %20-blue" height=40px>

### With [ALIAS](#-) (כינוי) we can give a name to our new COLUMN for exapmle : 
* We have the following  Query, the new column added is [(points+10)*100](#-)

```sql
SELECT 
    last_name, 
    first_name, 
    points , 
    (points+10 ) * 100
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716581-48f25a4e-1b20-4fe0-91de-d0cd01d2d890.png)

Let's give it an [ALIAS](#-) , as follows:

```sql
SELECT 
    last_name, 
    first_name, 
    points , 
    (points +10) * 100 AS discount_factor
FROM customers;
![image](https://user-images.githubusercontent.com/36256986/163716599-b3369f4d-bcb6-4205-a3a2-a1a7f9cee605.png)

```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------
