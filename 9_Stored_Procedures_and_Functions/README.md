###### _

<img src="https://img.shields.io/badge/-9. Stored Procedures and Functions %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|     |[Introduction Stored Procedures](#Introduction)   |             
|  1  |[Creating Stored Pocedure](#Creating_Stored_Pocedure)   |             
|  2  |[2](#2)   |
|  3  |[3](#3)   | 
|  4  |[4](#4)   | 
|  5  |[5](#5)   | 
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

How to do that?
We can create a **_Stored Procedre_** by adding the ```CREATE PROCEDURE```

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
