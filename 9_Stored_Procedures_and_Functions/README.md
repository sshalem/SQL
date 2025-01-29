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
|  6  |[Procedure Return OUT Parameters](#Procedure_Return_OUT_Parameters)   | 
|  7  |[Variables](#Variables)   | 
|  8  |[Functions](#Functions)   | 
|  9  |[Postgresql Functions](#9_postgresql_functions)   | 
|     |9.1. [plpgsql Functions](#9_1_plpgsql_functions)   | 
|  10  |[Postgresql Stored Procedures](#9_postgresql_stored_procedures)   | 


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

We can also use Stored Procedures for [INSERT](#-) , [UPDATE](#-) or [DELETE](#-) data. </br>
1. We are going to create a procedure that **_UPDATE_** data 
2. We are going to do [Parameter Validation](#-) to ensure the Procedure doesn't accidently store BAD data in the DB.

Let's do it in 2 steps.

### [step 1 : UPDATE](#-)
Let's create a simple procedure that gets 3 parameters and **UPDATE** the DB:

```sql
DROP PROCEDURE IF EXISTS make_payment;

DELIMITER $$
CREATE PROCEDURE make_payment (
    invoice_id INT,
    payment_amount DECIMAL(9, 2),
    payment_date DATE
)
BEGIN
    UPDATE invoices i 
    SET 
	i.payment_total = payment_amount,
        i.payment_date = payment_date
	WHERE i.invoice_id = invoice_id;
END $$
DELIMITER ;
```

Let's run it , and update invoice_id=2 , payment=100 and date 2019-01-01:

```sql
CALL make_payment(2, 100, '2019-01-01');
```

![image](https://user-images.githubusercontent.com/36256986/165340666-449c7d2e-b0b3-429a-aa35-d3f9fb386414.png)

### [step 2: parameter validation](#-)

Now let's add paramete validatino , for example to payment_amount.

[SIGNAL](#-) - is like throwing an exceptin in JAVA. </br>
[SQLSTATE](#-) - code error to be thrown :
1. error code from [ORCALE](https://docs.oracle.com/cd/E15817_01/appdev.111/b31228/appd.htm)
2. error code from [IBM](https://www.ibm.com/docs/en/db2-for-zos/11?topic=codes-sqlstate-values-common-error)

```sql
DROP PROCEDURE IF EXISTS make_payment;

DELIMITER $$
CREATE PROCEDURE make_payment (
    invoice_id INT,
    payment_amount DECIMAL(9, 2),
    payment_date DATE
)
BEGIN
	IF payment_amount <=0 THEN
		SIGNAL SQLSTATE '22003' SET MESSAGE_TEXT = 'Invalid payment_amount';
	END IF;
	UPDATE invoices i 
    SET 
	 i.payment_total = payment_amount,
        i.payment_date = payment_date
	WHERE i.invoice_id = invoice_id;
END $$
DELIMITER ;
```

Let's run it , and update invoice_id=2 , payment=-100 and date 2019-01-01:
Since payment is (-100) it should throw an exception error

```sql
CALL make_payment(2, -100, '2019-01-01');
```

![image](https://user-images.githubusercontent.com/36256986/165345850-9fa19edb-3468-43fa-8b4f-f35fbec781a5.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Procedure_Return_OUT_Parameters

<img src="https://img.shields.io/badge/-6. Procedure Return OUT Parameters %20-blue" height=40px>

With Procedures we can also return vlaues to the calling program. </br>
Lets see how to do it. </br>
The parameters that I return I add the **OUT** keyword.</br>
I need to assign each column to an **OUT PARAMETER** 


```sql
DROP PROCEDURE IF EXISTS get_unpaid_invoices_for_client;

DELIMITER $$
CREATE PROCEDURE get_unpaid_invoices_for_client (
    client_id INT,
    OUT invoices_count INT,
    OUT invoices_total DECIMAL(9, 2)    
)
BEGIN
    SELECT 
	COUNT(*),
       	SUM(invoice_total)
    INTO 
	invoices_count,
       	invoices_total
    FROM invoices i
    WHERE i.client_id = client_id AND payment_total = 0;        
END $$
DELIMITER ;
```

To run the Procedure need to do the following:
1. SET the OUT parameters with @ sign and assign 0 to them. (Since they are INT and DECIMAL) - Execute the SET @ lines (see **Variables** Section SET @ Variables).
2. CALL the procedure and add the SET @ parameters - Run the CALL  
3. Execute the ```SELECT @invoices_count, @invoices_total``` 

```sql
SET @invoices_count = 0;
SET @invoices_total = 0;
CALL get_unpaid_invoices_for_client(3, @invoices_count, @invoices_total);
SELECT @invoices_count, @invoices_total;
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Variables

<img src="https://img.shields.io/badge/-7. Variables %20-blue" height=40px>

We have following types of variables :
* [User or Session Variables](#-)  - for example ```SET @invoices_count = 0``` </br>
This variables will be in memory for the entire clients SESSION. when client disconnects fromMySql this variables are FREE
* [Local Varibales](#-) - this variable is defines inside a Function or Stored Procedure. Quiet often we use calculations in Store Procedures

### [example](#-)

Here I declare  LOcal variables. I can assign a DEFAULT value
```sql
DROP PROCEDURE IF EXISTS get_risk_factor;

DELIMITER $$
CREATE PROCEDURE get_risk_factor ()
BEGIN
    -- I give a DEFAULT value of 0 otherwise it will be NULL
    DECLARE risk_factor DECIMAL(9,2) DEFAULT 0;
    
    -- I am not giving a DEFAULT value to invoices_total and invoices_count 
    -- variable because we'll set it using a SELECT statement
    DECLARE invoices_total DECIMAL(9,2) DEFAULT 0;
    DECLARE invoices_count DECIMAL(9,2) DEFAULT 0;
    
    SELECT 
	COUNT(*),
        SUM(invoice_total)
	INTO 
		invoices_count,
		invoices_total        
	FROM invoices i;
    
    SET risk_factor = invoices_total / invoices_count * 5;
    
    SELECT risk_factor;
END $$
DELIMITER ;
```

Execute the Procedure:

```sql
CALL get_risk_factor();
```

![image](https://user-images.githubusercontent.com/36256986/165377289-8bccb307-490d-4a03-8c00-3390295f4692.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### Functions

<img src="https://img.shields.io/badge/-8. Functions %20-blue" height=40px>

link to [Difference between Function to Stored Procedure](https://www.dotnettricks.com/learn/sqlserver/difference-between-stored-procedure-and-function-in-sql-server)</br>
link to [Stack overflow for difference between Functions and Procedures](https://stackoverflow.com/questions/2680745/whats-the-differences-between-stored-procedures-functions-and-routineshttps://stackoverflow.com/questions/2680745/whats-the-differences-between-stored-procedures-functions-and-routines)

1. function must return a value 
2. Functions can have only input parameters for it 
3. Functions can be called from Procedure whereas Procedures cannot be called from a Function
4. Function allows only SELECT statement in it (Not INSERT, UPDATE, DELETE)
5. Function can be embedded in a SELECT statement.
6. Function can be used in the WHERE/HAVING/SELECT section

Let's see how to CREATE Function.</br>
The syntax for creating a Function is pretty similar for Stored Procedures.</br>
The following is the syntax of CREATE FUNCTION statement :

Link to how to create [**Functions**](https://www.mysqltutorial.org/mysql-stored-function/)

```sql
DROP FUNCTION IF EXISTS name_of_function;

DELIMITER $$
CREATE FUNCTION name_of_function(
	parameter1,
	parameter2,…
)
RETURNS {datatype STRING|INTEGER|REAL|DECIMAL}
	[NOT] DETERMINISTIC 
	READS SQL DATA
	MODIFIES SQL DATA
BEGIN
	-- code of statements to be executed
END $$
DELIMITER ;
```

* [**RETURN Datatype**](#-)  – We can return any type of value from the execution of the function. The type of value that will be returned needs to be specified after the RETURN clause. Once, MySQL finds the RETURN statement while execution of the function, execution of the function is terminated and the value is returned.

* [**DETERMINISTIC**](#-) – The function can be either deterministic or non-deterministic which needs to be specified here. When the function returns the same value for the same values of parameter then it is called deterministic. However, if the function returns a different value for the same values of functions then we can call that function to be nondeterministic. When none of the types of function is mentioned, then MySQL will consider function to be NON-DETERMINISTIC by default.

### [Example 1](#-)

```sql
DROP FUNCTION IF EXISTS isEligible;

DELIMITER $$
CREATE FUNCTION isEligible(
	age INTEGER
)
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
	IF age > 18 THEN
		RETURN ("yes");
	ELSE
		RETURN ("No");
	END IF;
END$$
DELIMITER ;
```

How to execute a function :

```sql
SELECT isEligible(20); 
```

![image](https://user-images.githubusercontent.com/36256986/165621156-fa824081-902a-484e-af72-333468a69bdb.png)

### [Example 2](#-)

Let us consider some other example that involves returning the number of months between the current date and the supplied date. </br>
Our function will be as follows –

```sql
DROP FUNCTION IF EXISTS getMonths;

DELIMITER $$
CREATE FUNCTION getMonths(sampledate date) 
RETURNS INT DETERMINISTIC
BEGIN
	DECLARE currentDate DATE;
	SELECT current_date() INTO currentDate;
	RETURN (12 * (YEAR(currentDate) - YEAR(sampledate)) + (MONTH(currentDate) - MONTH(sampledate)));
END
$$
DELIMITER ;
```

Let's run to execute a function :

```sql
SELECT getMonths("2021-12-01");
```

![image](https://user-images.githubusercontent.com/36256986/165621995-9a404a1a-d52c-4847-801f-c2d7fa0c30ba.png)

### [Example 3](#-)

```sql
DROP FUNCTION IF EXISTS calcIncome;

DELIMITER //
CREATE FUNCTION calcIncome ( starting_value INT )
RETURNS INT
DETERMINISTIC
BEGIN

   DECLARE income INT;
   SET income = 0;

   label1: 
   WHILE income <= 3000 
   DO
     SET income = income + starting_value;
   END WHILE label1;

   RETURN income;
END; //
DELIMITER ;

SELECT calcIncome(100);
```

![image](https://user-images.githubusercontent.com/36256986/165622887-b2bfd185-05bf-44cd-93ee-96b37f709f60.png)

### [Example 4](#-)

```sql
DROP FUNCTION IF EXISTS CustomerLevel;

DELIMITER $$
CREATE FUNCTION CustomerLevel(credit DECIMAL(10,2)) 
RETURNS VARCHAR(20) DETERMINISTIC
BEGIN
    DECLARE customerLevel VARCHAR(20);

    IF credit > 50000 THEN
		SET customerLevel = 'PLATINUM';
    ELSEIF (credit <= 50000 AND credit >= 10000) THEN
        SET customerLevel = 'GOLD';
    ELSEIF credit < 10000 THEN
        SET customerLevel = 'SILVER';
    END IF;
	-- return the customer level
	RETURN customerLevel;
END$$
DELIMITER ;

SELECT CustomerLevel(15445.16);
```

![image](https://user-images.githubusercontent.com/36256986/165624820-904b2529-7818-4b52-91b2-c19c4a1300ae.png)

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>

```sql
DELIMITER $$
CREATE PROCEDURE InitializeDB(startNumber INT, endNumber INT)
BEGIN   
    
    DECLARE counter INT DEFAULT startNumber;
    DECLARE en INT DEFAULT endNumber;

    WHILE counter <= en DO
        insert into books_tb(bookname, author, book_image_url) values('בראשית', 'משה רבנו', 'book_bereshit');
        SET counter = counter + 1;
    END WHILE;

END$$
DELIMITER ;
```
[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)


--------------------------------------------------------------------------------------------------

###### 9_postgresql_functions

<img src="https://img.shields.io/badge/- 9. postgresql functions  %20-blue" height=40px>

- link Derek Banas  : https://www.youtube.com/watch?v=85pG_pDkITY&ab_channel=DerekBanas
- link from postgresql : https://www.postgresql.org/docs/current/xfunc-sql.html#XFUNC-SQL-FUNCTION-ARGUMENTS
- In this tutorial I will show how to use [Functions](#-) in postgresql
- Rules of QUery FUnctions :  https://www.postgresql.org/docs/8.3/xfunc-sql.html
- `BEGIN\END` - see link https://www.postgresql.org/docs/current/plpgsql-structure.html

1. The body of an SQL function must be a list of SQL statements separated by semicolons.
2. A semicolon after the last statement is optional.
3. Unless the function is declared to return void, the last statement must be a SELECT.
4. The syntax of the CREATE FUNCTION command requires the function body to be written as a string constant.
5. It is usually most convenient to use dollar quoting [`$$`](#-) (see Section 4.1.2.2) for the string constant
6. `BEGIN\END` - It is important not to confuse the use of BEGIN/END for grouping statements in PL/pgSQL with the similarly-named SQL commands for transaction control. PL/pgSQL's BEGIN/END are only for grouping.
7. 





### [1_Function](#-)

1. Open SQL editor , and type the following code below
2. Open the Functions folder and see it's empty since we didn't add any finction yet

![image](https://github.com/user-attachments/assets/7a7d8243-2008-4122-9935-bbaeb040f9f0)

- `CREATE OR REPLACE FUNCTION` - keywords for a function
- `fn_add_ints(int,int)` - function name, see convention where I use `fn` prefix , then have 2 paramters of `int`
- `Return int` - The return value that the function returns

```sql
CREATE OR REPLACE FUNCTION fn_add_ints(int,int) RETURNS int as
$body$
	SELECT $1 + $2;
$body$
LANGUAGE SQL

select fn_add_ints(5,7);
```

3. Select only the code of the function , and click on the [execute query](#-) button (this store the function in the [Functions](#-) folder)

![image](https://github.com/user-attachments/assets/07d873b3-4cbb-42af-83cb-f4de83f649a1)

- Messsage shows FUnction created

![image](https://github.com/user-attachments/assets/67fd0b87-8d6f-4b26-ab82-80936a1039ea)


4. Refresh the DB, Check the [Functions](#-) folder , see that function [fn_add_ints](#-) is added to it

![image](https://github.com/user-attachments/assets/f395cc82-0738-4c32-8d7e-095c726250b1)

5. Now lets call the function and run it, to call a function we use the [select[(#-) command

```sql
select fn_add_ints(5,7);
```

- Result :

![image](https://github.com/user-attachments/assets/9f2f7463-51b7-407b-8cce-9e517ae2ae19)



- Lets look on another code with with different syntax , that does the same.
- See that now I define the variables x, y as integers , wherease in prev example I used `$` with the position of the varaibale to assign it.

```sql
CREATE OR REPLACE FUNCTION fn_add_em(x integer, y integer) RETURNS integer AS 
$$
    SELECT x + y;
$$ LANGUAGE SQL;

SELECT add_em(1, 2) AS answer;
```

- I execute only the Function to have it in the FUnctions folder 

![image](https://github.com/user-attachments/assets/5a69de65-8a18-4e8e-a710-dfb9e0df3b5a)

- Execute the FUnction

```sql
SELECT add_em(1, 2) AS answer;
```

![image](https://github.com/user-attachments/assets/523e29e4-21db-4422-8f7d-8aa3eca1a8a5)









[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

###### 9_1_plpgsql_functions

<img src="https://img.shields.io/badge/- 9.1. plpgsql functions  %20-green" height=30px>

- In previous section I use the [`LANGUAGE SQL`](#-)
- In order to be able to use FUnctions in more en hanced way I will use [`LANGUAGE plpgsql`](#-)
- I also add `BEGIN\END` , and inside them I write the logic
- We can No longer use `SELECT` in the BEGIN/ END , instead we use `RETURN`

![image](https://github.com/user-attachments/assets/83b70e4b-eccc-4847-9d30-6566c9b79740)

```sql
CREATE OR REPLACE FUNCTION fn_name(parameter par_type) RETURNS ret_type AS 
$$
BEGIN
	-- LOGIC written here
END
$$ LANGUAGE plpgsql;
```

Usage with `plpgsql` , see how I use the RETURN key instead of the SELECT key

```sql
CREATE OR REPLACE FUNCTION fn_add_them(x integer, y integer) RETURNS integer AS 
$$
BEGIN
	RETURN x + y;
END
$$ LANGUAGE plpgsql;

SELECT fn_add_them(1, 2) AS answer;
```

![image](https://github.com/user-attachments/assets/307b0b09-c66c-40cb-b9d9-d33d76bd0c71)




[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------


###### 10_postgresql_stored_procedures

<img src="https://img.shields.io/badge/- 9. postgresql stored procedures  %20-blue" height=40px>

In the previous sections , I used MySql for stored procedures. </br>
Now I will use `Postgresql` for it. </br>

link : https://www.youtube.com/watch?v=yLR1w4tZ36I&ab_channel=techTFQ


- Procedures can do things which SQL queries cannot.
- Procedure can include:
1. SQL queries
2. DML, DDL, DCL, and TCL commands
3. Collection types
4. LOOP &  IF ELSE statements
5. Variables
6. Exception handling
7. ETC...

### [Syntax to create a procedure in postgreSQL](#-)

Basic syntax w/n varable passed:

```sql
create or replace procedure pr_name()
language plpgsql
as $$
begin
    procedure body - all logics occur;
end;
$$
```


Basic syntax w/n varable passed:

```sql
create procedure raise_notice() 
language plpgsql 
as $$
begin 
    raise notice 'shabtay shalem';
end;
$$;

call raise_notice();
```


Basic syntax with varable passed:

```sql
create or replace procedure raise_notice(s text) 
language plpgsql 
as $$
begin 
    raise notice '%', s;
end;
$$

call raise_notice('shalem');



create or replace procedure show_msg(s text ,e text) 
language plpgsql 
as $$
begin 
    raise notice '% %', s;
end;
$$

call show_msg('my first name is', 'karin');
```

For some reason thihs also works:

```sql
create or replace procedure show_msg(s text ,e text) 
language plpgsql 
as $$
begin 
    raise notice;
end;
$$

call show_msg('my first name is', 'karin');
```




[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

