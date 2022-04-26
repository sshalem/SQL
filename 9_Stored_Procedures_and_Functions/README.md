###### _

<img src="https://img.shields.io/badge/-9. Stored Procedures and Functions %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|     |[Introduction Stored Procedures](#Introduction)   |             
|  1  |[Creating Stored Pocedure](#Creating_Stored_Pocedure)   |             
|  2  |[Dropping Stored Pocedure](#Dropping_Stored_Pocedure)   |
|  3  |[Parameters](#Parameters)   | 
|  4  |[Parameters with default values](#Parameters_with_default_values)   | 
|  5  |[Parameters validation](#Parameters_validation)   | 
|  6  |[6](#6)   | 
|  7  |[7](#7)   | 


--------------------------------------------------------------------------------------------------

###### Introduction

<img src="https://img.shields.io/badge/- Introduction Stored Procedures  %20-blue" height=40px>

Let's say I have an application that has a DB. </br>
Where are we going to write this SQL statements? </br>
We are not going to write them in our application code for couple of reasons. </br>
One reason , it will make the App code messy and hard to maintain. </br>
For that reason we should put our SQL inside a [**_Stored Procedure_**](#-) or [**_Function_**](#-).</br>
(In Spring Boot It's pretty Easy since we only use the Queries in one place which is **_the Repository Class_**.)

![image](https://user-images.githubusercontent.com/36256986/165103485-63703d50-702e-483a-804f-afa321204775.png)

[**_Stored Procedure_**](#-) - Is a DataBase Object that contains a block of SQL code. I our App code we simply call these procedures, get or save the data. </br>

[**_Store and organize SQL_**](#-) -  **_Stored Procedure_** used for Store and organize SQL code.

[**_Faster_execution_**](#-) - **_Stored Procedure_** has other benefits , most DB management systems perform some kind of optimization to the code in **_Stored Procedure_**. So the SQL code in **_Stored Procedure_** can sometimes be **_executed faster_**.

[**_Data Security_**](#-) - Also, just like **_VIEWS_** , **_Stored Procedure_** allow us to enforce data security. </br>
* For exmple: </br>
you can remove direct access to the tables, and allow various operations like inserting, updating, adn deleting data to inform your **_Stored Procedure_**. Then we can decide who can execute which **_Stored Procedure_** , and this will limit what user can do with our data.

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Creating_Stored_Pocedure

<img src="https://img.shields.io/badge/-1. Creating Stored Pocedure  %20-blue" height=40px>

We want to Store this Query in a **_Stored Procedre_**

```sql
SELECT * FROM clients;
```
### [**Create Stored Procedure**](#-)

[Note](#-): With **MySql** we have to change the **DELIMITER**.

```sql
-- We have to change the default DELIMITER from (semicolon ;)
-- to anything that MySql doesn't use
-- The Convention is $$ (2 dollars sign)
-- We have to Add a DELIMITER so the Stored Procedure will run as a single unit
DELIMITER $$
CREATE PROCEDURE get_clients()
BEGIN
  -- This is the Body of the Stored Procedure
  SELECT * FROM clients;
END$$
-- We have to change the DELIMITER back to default (semicolon)
DELIMITER ;
```

Then execute the code , Refersh the DB, nnow we see the Stored procedure in the DB.

![image](https://user-images.githubusercontent.com/36256986/165128817-b2ab4025-e187-453a-befc-295c40799785.png)

### [**Call store procedure as follows:**](#-)


* Most of the time , calling a **Stored Procedure** is someting that we do in our App (like JAVA ,Python ,C#), But there are times where we want to call **Stored Procedure** in our SQL code.

```sql
CALL get_clients();
```

### [**Exercise**](#-)

* Create Stored Procedure called **get_invoices_with_balance** </br>
to return all the invoices with a balance > 0.

```sql
DELIMITER $$
CREATE PROCEDURE get_invoices_with_balance()
BEGIN
	SELECT * 
	FROM invoices
	WHERE invoice_total - payment_total > 0;
END $$
DELIMITER ;
```

### [**CREATE PROCEDURE using MySql Workbench**](#-)

This is how to create procedure With MySql 

![image](https://user-images.githubusercontent.com/36256986/165173144-5724f5ce-cb2b-4fc8-83d5-20ed3f4d33dd.png)

Following window is open with already a ready template for Creating Procedure.
Just need to write our query and click on APply

![image](https://user-images.githubusercontent.com/36256986/165173187-32791b63-2ac9-4c59-853a-9ac3cedac47d.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Dropping_Stored_Pocedure

<img src="https://img.shields.io/badge/-2. Dropping Stored Pocedure  %20-blue" height=40px>

Use following command to DROP procedure

```sql
DROP PROCEDURE IF EXISTS get_clients;
```
[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Parameters

<img src="https://img.shields.io/badge/-3. Parameters  %20-blue" height=40px>

We can create a **Stored Procedure** that get parameters.</br>
See the example below where we pass only one parameter.

```sql
DROP PROCEDURE IF EXISTS get_clients_by_state;

DELIMITER $$
CREATE PROCEDURE get_clients_by_state(state CHAR(2))
BEGIN
	SELECT * 
	FROM clients c
	WHERE c.state = state;
END$$
DELIMITER ;

CALL get_clients_by_state('NY');
```

### [**Exercise**](#-)

Write a Stored Procedure to return invoices for a given client.</br>
call it **get_invoices_by_client**, give it a client_id parameter.

```sql
DROP PROCEDURE IF EXISTS get_invoices_by_client;

DELIMITER $$
CREATE PROCEDURE get_invoices_by_client(client_id INT)
BEGIN
	SELECT * 
	FROM invoices i    
	WHERE i.client_id = client_id;
END$$
DELIMITER ;

CALL get_invoices_by_client(1);
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Parameters_with_default_values

<img src="https://img.shields.io/badge/-4. Parameters with default values  %20-blue" height=40px>

### [**Example 1**](#-)

In this example we create a procedure , with default value for NULL.</br>
If NULL is entered it will serach for 'CA'

```sql
DROP PROCEDURE IF EXISTS get_clients_by_state;

DELIMITER $$
CREATE PROCEDURE get_clients_by_state(state CHAR(2))
BEGIN
	-- Give a Default value
        IF state IS NULL THEN
		SET state = 'CA';
	END IF;
	SELECT * FROM clients c
	WHERE c.state = state;
END$$
DELIMITER ;

CALL get_clients_by_state(NULL);
```

### [**Example 2**](#-)

In this example we create a procedure , with default value for NULL.</br>
If NULL is entered it will query * from clients.
In this example I use the IF ELSE 

```sql
DELIMITER $$
CREATE PROCEDURE get_clients_by_state(state CHAR(2))
BEGIN
	-- Give a Default value
    	IF state IS NULL THEN
		SELECT * FROM clients;
	ELSE        
		SELECT * FROM clients c
		WHERE c.state = state;
	END IF;	
END$$
DELIMITER ;

-- Run both CALL's seperatly to check how IF ELSE is working
CALL get_clients_by_state(NULL);
CALL get_clients_by_state('NY');
```

### [**Example 3**](#-)

Let's modify the exapmle above to be less verbose. 

```sql
DROP PROCEDURE IF EXISTS get_clients_by_state;

DELIMITER $$
CREATE PROCEDURE get_clients_by_state(state CHAR(2))
BEGIN
	SELECT * FROM clients c
	WHERE c.state = IFNULL(state, c.state);	
END$$
DELIMITER ;

CALL get_clients_by_state(NULL);
CALL get_clients_by_state('NY');
```

### [**Exercise**](#-)

* Write a procedure called **get_payments** , with two parameters:</br>
client_id => INT , payment_method_id => TINYINT

```sql
DROP PROCEDURE IF EXISTS get_payments;

DELIMITER $$
CREATE PROCEDURE get_payments(
    client_id INT,
    payment_method_id TINYINT    
)
BEGIN
    SELECT * 
    FROM payments p
    WHERE
        p.client_id = IFNULL(client_id ,p.client_id) AND 
        p.payment_method = IFNULL(payment_method_id, p.payment_method);			
END$$
DELIMITER ;

CALL get_payments(NULL , NULL);
CALL get_payments(5 , NULL);
CALL get_payments(5 , 2);
CALL get_payments(NULL , 2);

```


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Parameters_validation

<img src="https://img.shields.io/badge/-5. Parameters validation %20-blue" height=40px>


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
