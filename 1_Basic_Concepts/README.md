###### _

<img src="https://img.shields.io/badge/-Basic Concepts%20-blue" height=60px>

|     |  Subject           |
|:---:|:------------------------------| 
|  1  |[Data Types](#1)   | 
|  2  |[Primary Key [PK]](#2)   | 
|  3  |[a](#3)   | 
|  4  |[a](#4)   | 
|  5  |[a](#5)   | 

###### 1

<img src="https://img.shields.io/badge/-1. Data Types %20-blue" height=40px>

![dataTypes](https://user-images.githubusercontent.com/36256986/158463506-c95ccea7-e00b-4b3f-be5b-fab4d909a601.png)

INT - whole Number</br>
	INT(11)  - number in length of 11 numbers</br>
	
DECIMAL(M,N) - DECIMAL Numbers</br>
	DECIMAL(3,6) - 465.789465  </br>
	
VARCHAR(l)  - String  , l -maximum length</br>
	VARCHAR(50) - Max length of 50 characters </br>
	


[Question:](#-)</br>
	What the differnece between VARCHAR (50) and CHAR(50)?

[Answer:](#-)</br>
	VARCHAR(50) - if I have a String less than 50 characters, the MySql engine won't complete it to 50 </br>
	CHAR(50) -  if I have a String less than 50 characters, the MySql engine completes it to 50 which is a waist </br>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. Primary Key [PK] %20-blue" height=40px>

![image](https://user-images.githubusercontent.com/36256986/158466392-e0a7b9bb-cead-4d18-a8fa-d56404f07731.png)

Primary Key can be composed of set of columns :

![image](https://user-images.githubusercontent.com/36256986/158466486-d56c6d70-2fe4-4d4c-9731-953f060b4501.png)

![image](https://user-images.githubusercontent.com/36256986/158466515-196a424c-68a6-43e9-a0aa-a8f7ecc583e9.png)


```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

Composite Key means, we composite a primary key from 2 FK columns .
In the exapmle below we have 3 tables:

	1. Employee Table - has PK of emp_id and 2 FK of branch_id & super_id 
	2. Client table - has PK of client_id and FK of branch_id
	3. Works_With table - has composed key mad of 2 FK columns  emp_id & client_id 

Question:
	Why we compose 2 primary keys ?
Answer:
	Because Only together they uniquely identify the sup


We can see in the table Works_With , that the primary key is composed of 2 columns 


![image](https://user-images.githubusercontent.com/36256986/158467407-75e97642-ec35-4f2b-add5-5af0b39894d8.png)



[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 4

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 5

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 6

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 7

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 8

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 9

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 10

<img src="https://img.shields.io/badge/-23 %20-blue" height=40px>

```java
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
