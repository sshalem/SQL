###### _
<img src="https://img.shields.io/badge/-2_DataBase_and_TABLE %20-blue" height=60px>

|     |  Subject           |          |
|:---:|:------------------------------|:-------| 
|  1  |[CREATE DATABASE](#1)   | 
|  2  |[USE keyword](#2)       | 
|  3  |[CREATE TABLE](#3)      | 
|     |                        |  [TABLE constraints](#3-1)  |
|  4  |[DESCRIBE command](#4)  |  
|  5  |[DROP (delete)](#5)    | 
|  6  |[ALTER TABLE … ADD/DROP](#6)    | 
|  7  |[Keys - Tables with MySql](#7)    | 
|  8  |[INSERT](#8)    | 
|     |                        |  [INSERT Single row](#8-1)  |
|     |                        |  [INSERT multiple rows](#8-2)  |
|     |                        |  [INSERT hierarchical rows](#8-3)  |
|  9  |[copy of TABLE](#9)    | 
|  10 |[UPDATE](#10)    | 
|     |                     |  [UPDATE Single row](#10-1)  |
|     |                     |  [UPDATE multiple rows](#10-2)  |
|     |                     |  [UPDATE with SubQuery](#10-3)  |
|  11 |[DELETE](#11)    | 

###### 1

<img src="https://img.shields.io/badge/-1. CREATE DATABASE %20-blue" height=40px>

Command for **_creating DB_**:

```sql
CREATE DATABASE orders_tb;
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. USE keyword  %20-blue" height=40px>

The keyword USE chooses the DB we want to work with.</br>
this command will highlight the DB we chose.</br>

```java
USE orders_tb;
```

![image](https://user-images.githubusercontent.com/36256986/158583497-9fe9feb8-fd27-4634-8c0c-6b22587ff71a.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-3. create Table %20-blue" height=40px>

### Let's create the following table in DB:

<img src="https://user-images.githubusercontent.com/36256986/158580714-9527a8a7-efd6-4cb7-9f9a-d0ac62c6203f.png" width=300px height=150px>

```sql
CREATE TABLE student(
    student_id INT PRIMARY KEY,
    name VARCHAR(20),
    major VARCHAR(20)    
);
```

### Another way to define the [PRIMARY KEY](#-):

```sql
CREATE TABLE student(
    student_id INT,
    name VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY (student_id)
);
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3-1

<img src="https://img.shields.io/badge/-3.1 TABLE constrains %20-blue" height=40px>

Let's see the following table without constraints: </br>

```sql
CREATE TABLE student(
    student_id INT,
    name VARCHAR(20),
    city VARCHAR(20),
    address VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY (student_id)
);
```

Now we add constraints to it:

Constraints words are: 
- AUTO_INCREMENT (For primary key)
- NOT NULL
- UNIQUE
- DEFAULT

```sql
CREATE TABLE student(
    student_id INT AUTO_INCREMENT,
    name VARCHAR(20) NOT NULL,
    city VARCHAR(20),
    address VARCHAR(20) UNIQUE,
    major VARCHAR(20) DEFAULT 'undecided',
    PRIMARY KEY (student_id)
);
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 4

<img src="https://img.shields.io/badge/-4. DESCRIBE command %20-blue" height=40px>

With **DESCRIBE** command we can see the definition of each column .

Let's look at the table we created:

```sql
CREATE TABLE student(
    student_id INT,
    name VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY (student_id)
)
```

The following select command will show us the data in the table:

```sql
SELECT * FROM student;
```

![image](https://user-images.githubusercontent.com/36256986/162806197-60be545f-8296-4682-8394-b49e48bbed9d.png)

The **_DESCRIBE_** command will show us the definition of each column.

```sql
DESCRIBE student;
```

![image](https://user-images.githubusercontent.com/36256986/162806296-ed159600-7347-4acb-8659-a853a594b384.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 5

<img src="https://img.shields.io/badge/-5. DROP (delete) %20-blue" height=40px>

DROP command is actually deleting the table.

```sql
DROP TABLE student;
```

![image](https://user-images.githubusercontent.com/36256986/162806657-55d36206-98cc-430e-9e40-5a9227e06330.png)


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 6

<img src="https://img.shields.io/badge/-6. ALTER TABLE … ADD/DROP %20-blue" height=40px>

With **ALTER** command we can add a new field to an existing table. </br>
Let say we created the following table:

```sql
CREATE TABLE student(
    student_id INT,
    name VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY (student_id)
);
```

**DESCRIBE** shows us following fields:

```sql
DESCRIBE student;
```

![image](https://user-images.githubusercontent.com/36256986/162807137-b95b50be-02b8-44d0-bc30-dca7e1d7460d.png)

```sql
ALTER TABLE student ADD gpa DECIMAL(3,2);
```

![image](https://user-images.githubusercontent.com/36256986/162807204-55cd37b9-0075-4153-9cc8-7fc21d054f82.png)

We can see the gpa Field is added to table.

To remove a column from table we use following command:

```sql
ALTER TABLE student DROP gpa;
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 7

<img src="https://img.shields.io/badge/-7. Keys ,Tables with MySql %20-blue" height=40px>

Let's look in the following tables and see how the keys are define:

### [Table with [PK] only](#-)

We can see that customers table has only PK (1 PK not composite)

[Customer table:](#-)

![image](https://user-images.githubusercontent.com/36256986/163399417-e93f1777-8689-4cc0-ba2d-a64f00a7bfb4.png)

```sql
DESCRIBE customers;
```

![image](https://user-images.githubusercontent.com/36256986/163399507-c13b9c48-1ea9-4d23-ae65-38a52cdc62db.png)

![image](https://user-images.githubusercontent.com/36256986/163399519-a5047fe7-43f4-49bf-b0a0-90009ee2dae1.png)


### [Table with [PK] and [FK's]](#-)

[Orders table:](#-)

We can see that customers table has :

- order_id  :  [PK](#-)
- customer_id  : [FK](#-)
- status   :  [FK](#-)
- shipper_id   :  [FK](#-)

![image](https://user-images.githubusercontent.com/36256986/163400664-daa99aaa-ed86-4a83-a469-0f76369c3582.png)

![image](https://user-images.githubusercontent.com/36256986/163400679-5d23457f-486c-411f-b8fe-65dbf6b7bcf3.png)

![image](https://user-images.githubusercontent.com/36256986/163400692-a7f5e33b-c88d-4b59-9116-9384b0be844a.png)


### [Table CK (as a PK)](#-)

We can see following table has 2 PK , but they are actually a Composite of 2 FK :

[order_items table:](#-)

![image](https://user-images.githubusercontent.com/36256986/163400876-5e8f3436-2ac2-4a91-8dfc-5a017f5d994e.png)

The 2 PK we see here They are marked as PK because they are composite Key:

![image](https://user-images.githubusercontent.com/36256986/163400926-4d866c0b-b757-40c7-916d-ed3a9e0215ae.png)

Here we can see that they really a FK and not a PK, </br>
Only together the compose a PK. 

![image](https://user-images.githubusercontent.com/36256986/163401002-80fe9481-af4b-4eed-9c43-12946f44a422.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 8

<img src="https://img.shields.io/badge/-8. INSERT %20-blue" height=40px>

###### 8-1

<img src="https://img.shields.io/badge/-8.1 INSERT single row %20-yellow" height=30px>

Let's see the attributes of our Customer Table:

![image](https://user-images.githubusercontent.com/36256986/163402962-a013163e-5fb9-4006-8e60-abf874502d38.png)

If we want to ISERT a row in DB we do the following: </br>
Since the first Field is a **PK** of the table and it is **_AI (Auto Increment)_** , best practice is to set it as DEFAULT:

```sql
INSERT INTO customers
VALUES (DEFAULT, 'shabtay' , 'shalem' , '1977-01-29' , '052-8855371' , 'Menachem begin 15' , 'HOLON' , 'IL' , 654798);
```

![image](https://user-images.githubusercontent.com/36256986/163403202-03ad58a3-0576-4feb-b7c9-dcb0d5373294.png)

We can also make the following INSERT because the birth_date & phone can have a default value of NULL and points default value of 0.

```sql
INSERT INTO customers
VALUES (DEFAULT, 'temp', 'temp', DEFAULT, DEFAULT , 'Menachem begin 15' , 'HOLON' , 'IL' , DEFAULT);
```

Or we can write it following way , which INSERT the same record to Table.

```sql
INSERT INTO customers
VALUES (DEFAULT, 'temp', 'temp', NULL , NULL , 'Menachem begin 15' , 'HOLON' , 'IL' , 0);
```

Since we have DEFAULT values , we can write INSERT statement in a shorter way:

```sql
INSERT INTO customers (
	first_name,
	last_name,
	address,
	city ,
	state)
VALUES ('temp' ,
	'temp' ,  
	'Menachem begin 15' , 
	'HOLON', 
	'IL');
```

###### 8-2

<img src="https://img.shields.io/badge/-8.2 INSERT multiple rows %20-yellow" height=30px>

Let's use the shippers table to see how to add multiple rows. </br>
Has AI PK (AUTO INCREMENT) </br>
No default value for the name field. </br>

![image](https://user-images.githubusercontent.com/36256986/163404017-4b8f5096-ba48-4295-b0df-b16010a87e60.png)

```sql
INSERT INTO shippers(name)
VALUES ('shippers1'),
       ('shippers2'),
       ('Shippers3'),
       ('Shippers4'),
       ('Shippers5');
```

![image](https://user-images.githubusercontent.com/36256986/163404277-0b0ae02b-8ba6-4d43-a12a-da806400c49c.png)

###### 8-3

<img src="https://img.shields.io/badge/-8.3 INSERT hierarchical rows %20-yellow" height=30px>

Let's look in the following tables:
1. Orders
2. Order_items

### [Order](#-)

![image](https://user-images.githubusercontent.com/36256986/163405529-24dede87-f7fa-4f1c-918a-4c12bb4e2042.png)


### [Order_items](#-)

![image](https://user-images.githubusercontent.com/36256986/163405557-2687337a-05e3-4daa-8a1a-ccf3c6ae3917.png)

We assign to : </br>
	customer_id  (There is already customer_id =1 , we just add to it another Order_id)</br>
	order_date, </br>
	status </br>
	
```sql
INSERT INTO orders(customer_id, order_date, status) 
VALUES (1, '2019-01-27', 1);

INSERT INTO order_items 
VALUES 
	(LAST_INSERT_ID() , 1, 1, 3.95),
	(LAST_INSERT_ID() , 2, 1, 3.95);
```

![image](https://user-images.githubusercontent.com/36256986/163406054-70dd0f70-f6ea-47b9-aeaf-a397bfdd77bc.png)

The new Tables as follows:

### [Order Table](#-)

![image](https://user-images.githubusercontent.com/36256986/163406145-fddde294-da32-4896-b5ab-ae0d9bce560b.png)

### [Order_items_Table](#-)

![image](https://user-images.githubusercontent.com/36256986/163406253-10a040ac-427d-4232-a369-9483e6d80ec1.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 9

<img src="https://img.shields.io/badge/-9. copy of TABLE %20-blue" height=40px>

We can create a copy of a table .
Let's see 2 different approach for creating copy of orders table.

### [Approch 1](#-)

We use the following command:

```sql
CREATE TABLE orders_archived AS (SELECT * FROM orders);
```

It means :
1. Create table with name of orders_archived
2. We run a Sub query to select all records from orders table

Let's Refresh the DB , we can see that a new Table created :

![image](https://user-images.githubusercontent.com/36256986/163406968-d070b211-d609-4945-9f9d-55f35d9b9bb0.png)

![image](https://user-images.githubusercontent.com/36256986/163407024-ce8eaa1f-2e06-4abe-8e33-0a3d5d44bf05.png)

![image](https://user-images.githubusercontent.com/36256986/163407055-b688704a-6358-4a14-af97-2f96442b6311.png)

```sql
CREATE TABLE orders_archived AS 
(SELECT * FROM orders WHERE order_date <= '2019-01-01');
```

### [Approch 2](#-)

Let's [Truncate](#-) the orders_archived table (**Truncate** deletes all records from Table but Doesn't Drop the table)

```sql
INSERT INTO orders_archived (SELECT * FROM orders);
```

In this Approach , we can INSERT into orders_archived only the values we want 

```sql
INSERT INTO orders_archived
(SELECT * FROM orders  WHERE order_date <= '2019-01-01');
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 10

<img src="https://img.shields.io/badge/-10. UPDATE %20-blue" height=40px>

###### 10-1

<img src="https://img.shields.io/badge/-10.1 UPDATE single row %20-yellow" height=30px>

Let's see how to update a Single row with data.</br>
We want to update 2 columns in a Table of Invoice 
	1. payment_total 
	2. payment_date
	
Before Update:

![image](https://user-images.githubusercontent.com/36256986/163468664-4c538cf2-5f09-4a64-ae83-09e90b8b2728.png)


UPDATE :

```sql
UPDATE invoices
SET
	payment_total = 10 , 
	payment_date = '2020-01-29'
WHERE invoice_id = 1;
```

After Update:

![image](https://user-images.githubusercontent.com/36256986/163468750-a46ad5cc-a7ab-4067-86ac-9b6999e2184a.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

###### 10-2

<img src="https://img.shields.io/badge/-10.2 UPDATE multiple rows %20-yellow" height=30px>

Let's say we want to change multiple records for client_id number 3 :

![image](https://user-images.githubusercontent.com/36256986/163468861-e3f225be-9d54-49b0-ac3d-ac5d7611594e.png)

We need to change in MySql workbench the following feature.

Why? </br>
Because MySql workbench works in a safe mode , so it will only update a single record.

So need to change this safe mode, so it will be able to update multiple records. </br>

Disable the Safe Update: </br>
	EDIT -> Preferences -> SQL Editor -> Disable safe update

![image](https://user-images.githubusercontent.com/36256986/163469017-789e72b3-f36d-4069-9a47-1c6bf3ec453a.png)

Disable the Safe Update

![image](https://user-images.githubusercontent.com/36256986/163469047-783f8186-e4ea-4537-b197-fb8ce5581c96.png)

```sql
UPDATE invoices
SET
	payment_total = invoice_total * 0.5, 
	payment_date = due_date
WHERE client_id = 3;
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

###### 10-3

<img src="https://img.shields.io/badge/-10.3 UPDATE with SubQuery %20-yellow" height=30px>

A SubQuery s a SELECT statement that is inside another SQL statement.</br>
Instead of Hard code of client_id=3, I runSQL query on clients table to search for the client_id. </br>
For that I use a Subquery as in the example below:

```sql
UPDATE invoices
SET
	payment_total = invoice_total * 0.5,
	payment_date = due_date
WHERE client_id = (
	SELECT client_id 
	FROM clients
	WHERE name = 'Myworks');
```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)


----------------------------------------------------------------------------------

###### 11

<img src="https://img.shields.io/badge/-11. DELETE %20-yellow" height=30px>

DELETE command:

```sql
DELETE FROM invoices WHERE client_id = 2;
```

Using Subquery:

```sql
DELETE FROM invoices 
WHERE client_id = 
	(SELECT client_id 
	 FROM clients 
	 WHERE name='Myworks');
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
