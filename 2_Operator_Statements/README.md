###### _

<img src="https://img.shields.io/badge/-3_Operator Statements%20-blue" height=60px>

|     |  Subject           |             | 
|:---:|:------------------------------|:------| 
|  1  |[USE](#1)   |    |
|  2  |[SELECT](#2)   |     |
|     |2.1.            |[SELECT with Arithmetic *  /  +  -  %](#2-1) |
|  3  |[ALIAS](#3)   |           |
|  4  |[DISTINCT](#4)   |        |
|  5  |[WHERE](#5)   |     |
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

![image](https://user-images.githubusercontent.com/36256986/163716599-b3369f4d-bcb6-4205-a3a2-a1a7f9cee605.png)

```sql
SELECT 
    last_name, 
    first_name, 
    points , 
    (points +10) * 100 AS discount_factor
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716625-abb97057-6aa8-440e-b51f-0b6e6f439fb2.png)

Let's give it an [ALIAS](#-)  **w/o underscore** , as follows:
* We need to add quotes to it (Can be single quote or double quotes)

```sql
SELECT 
    last_name, 
    first_name, 
    points , 
    (points +10) * 100 AS 'discount factor'
FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716674-56c045d9-5687-4d98-8208-a6ddd6f394de.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 4

<img src="https://img.shields.io/badge/-4. DISTINCT %20-blue" height=40px>

With DISTINCT keyword we can remove duplicates.</br>
Let's look at customers table , we can see we have state 'VA' 3 times :

![image](https://user-images.githubusercontent.com/36256986/163716791-f7f36dff-52a0-4c54-a4b7-b4455202cd98.png)

Let's query only the state :

```sql
SELECT state FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716845-dff907cc-97d5-4e49-a7e8-7ba0c4df548d.png)

To remove duplicates we use the keyword DISTINCT :

```sql
SELECT DISTINCT state FROM customers;
```

![image](https://user-images.githubusercontent.com/36256986/163716872-9e9e3244-28a4-44da-b789-0b783d1982f3.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 5

<img src="https://img.shields.io/badge/-. WHERE  %20-blue" height=40px>

We use the WHERE clause to filter data.</br>
Comparison operators: 
* Greater than:   [>](#-)
* Greater than or equal to:   [>=](#-)
* Less than:   [<](#-)
* Less than or equal to:   [<=](#-)
* Equal:   [=](#-)
* Not equal:   [<>](#-)
* Not equal:   [!=](#-)

Let's look at the following examples:

```sql
SELECT * FROM customers WHERE points > 3000;
```

![image](https://user-images.githubusercontent.com/36256986/163717023-660fbce0-02cf-4dfd-bbc7-9afe78861404.png)

```sql
SELECT * FROM customers WHERE state = 'VA';
```

![image](https://user-images.githubusercontent.com/36256986/163717058-0daf0397-2b95-4bd1-87e3-3be8175de139.png)

```sql
SELECT * FROM customers WHERE state != 'VA';
```

![image](https://user-images.githubusercontent.com/36256986/163717078-4c10fdcd-a23a-423c-abd9-f22034931b1f.png)


![image](https://user-images.githubusercontent.com/36256986/163717088-792becdc-8d90-4c4b-88f9-2b49010b925f.png)

```sql
SELECT * FROM customers WHERE birth_date > '1990-01-01';
```

![image](https://user-images.githubusercontent.com/36256986/163717112-e0378bb5-e6d9-4eb5-ba14-0ae886c11a64.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 6

<img src="https://img.shields.io/badge/-6. Logical Operators AND, OR, NOT  %20-blue" height=40px>

### [AND operator](#-)

```sql
SELECT * 
FROM customers 
WHERE birth_date > '1990-01-01' AND points > 1000;
```

![image](https://user-images.githubusercontent.com/36256986/163731743-444454b4-6713-4c18-b4a8-0def86ea83a2.png)

### [AND with NOT operator](#-)

```sql
SELECT * 
FROM customers 
WHERE NOT (birth_date > '1990-01-01' AND points > 1000);
```

![image](https://user-images.githubusercontent.com/36256986/163731768-ec151146-55aa-4058-bfe7-a8532114ee26.png)

### [OR operator](#-)

```sql
SELECT * 
FROM customers 
WHERE birth_date > '1990-01-01' OR points > 3000;
```

![image](https://user-images.githubusercontent.com/36256986/163731804-62c86a0c-a68c-49e2-9d4b-650fccf37117.png)


### [OR with NOT operator](#-)

```sql
SELECT * 
FROM customers 
WHERE NOT ( birth_date > '1990-01-01' OR points > 3000);
```

![image](https://user-images.githubusercontent.com/36256986/163731818-13b0b7f0-f56a-4a13-8b0f-7d1faeff8ecd.png)

### [MULTI operators](#-)

```sql
	SELECT * 
	FROM customers 
	WHERE birth_date > '1990-01-01' OR
		  (points > 3000 AND state = 'VA');
```

![image](https://user-images.githubusercontent.com/36256986/163731842-d1ded73b-931e-40e1-bd47-87fb049fa5ac.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

Example:

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------


###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

Example:

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------


###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

Example:

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------


###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

Example:

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------


###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

Example:

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------


###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

Example:

```sql
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------
