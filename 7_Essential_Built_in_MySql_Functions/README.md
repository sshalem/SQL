###### _

<img src="https://img.shields.io/badge/-7. Essential Built in MySql Functions %20-blue" height=60px>

### Essential Built in MySql Functions for working with:
1. [**_Numeric_**](#-)
2. [**_Date time_**](#-)
3. [**_String values_**](#-)

|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|  1  |[Numeric Functions](#1)   |             
|  2  |[String Functions](#2)   |
|  3  |[Date and Time Functions](#3)   | 
|  4  |[Formatting Dates and Times](#4)   | 
|  5  |[Calculating Dates and Times](#5)   | 
|  6  |[IFNULL and COALESCE Functions](#6)   | 
|  7  |[IF Function](#7)   | 
|  8  |[CASE Operator](#8)   | 



--------------------------------------------------------------------------------------------------

###### 1

<img src="https://img.shields.io/badge/-1.  %20-blue" height=40px>

### Most useful [Numeric](#-) functions:

```sql
-- will round to 5.2
SELECT ROUND(5.24, 1);

-- will round to 5.3
SELECT ROUND(5.27, 1);

-- give number 5.734
SELECT TRUNCATE(5.73456, 3);

-- Returns smallest integer that is greater than or equal to the number.
-- Returns 6
SELECT CEILING(5.73654);

-- Returns largest integer that is less than or equal to the number.
-- Returns 5
SELECT FLOOR(5.73654);

-- for calc the absolute value of a number.
-- return 5.73
SELECT ABS(-5.73);

-- Rand generate random floating point number between 0 and 1
SELECT RAND();
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 2

<img src="https://img.shields.io/badge/-2. String Functions %20-blue" height=40px>

### Most useful [String](#-) functions:

```sql
-- retruns the legth of the string
SELECT LENGTH('sky');

-- Convert the String to upper case
SELECT UPPER('sky');

-- Convert the String to upper case
SELECT LOWER('SKy');

-- Removing unecessery space
SELECT TRIM('    SkY   ');

-- LTRIM refers to LEFT TRIM - Removing unecessery space from left side of String
SELECT LTRIM('   SKy');

-- RTRIM refers to RIGHT TRIM - Removing unecessery space from right side of String
SELECT RTRIM('SKy     ');

-- Returns the first 4 letters from the left
SELECT LEFT('kindergarden',4);

-- Returns the first 4 letters from the right
SELECT RIGHT('kindergarden',4);

-- This will return 'ergard' 
-- From the fifth letter , return the next 6 letters
-- SELECT SUBSTRING('String' ,start , length);
SELECT SUBSTRING('kindergarden' ,5 , 6);

-- returns the position of the first occurance of a character
-- Searching is not case sensitive
-- returns position 4
-- If character doesn't exist it returns 0
SELECT LOCATE('d', 'kindergarden');

-- This returns position 4 because the String starts from position 4
SELECT LOCATE('derg', 'kindergarden');

-- SELECT REPLACE(String, replace, value);
SELECT REPLACE('kindergarden', 'gar' , 's');

-- Combine 2 String to one String
-- returns firstlast
SELECT CONCAT('first','last');

SELECT CONCAT(first_name, '  ',  last_name) AS full_name
FROM customers;
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 3

<img src="https://img.shields.io/badge/-3. Date and Time Functions %20-blue" height=40px>

### Most useful [**_Date and Time_**](#-) functions:

### The following functions return  [**_Integers_**](#-):

```sql
-- Get current date & TIme
SELECT NOW();

-- Get only Current Date
SELECT CURDATE();

-- Get only current TIme
SELECT CURTIME();

-- ALl together will be presented in 3 columns
SELECT NOW() , CURDATE(), CURTIME();

-- Extract the year ,Month, Dayform NOW() Function
SELECT YEAR(NOW());
SELECT MONTH(NOW());
SELECT DAY(NOW());

-- Extract the Hour , Minute, Second form NOW() Function
SELECT HOUR(NOW());
SELECT MINUTE(NOW());
SELECT SECOND(NOW());
```

### The following functions return [**_Strings_**](#-):

```sql
SELECT DAYNAME(NOW());
SELECT MONTHNAME(NOW());
```

### The [**_EXTRACT()_**](#-) Function is part of the standard SQL language:

```sql
SELECT EXTRACT(DAY FROM NOW());
SELECT EXTRACT(MONTH FROM NOW());
SELECT EXTRACT(YEAR FROM NOW());
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 4

<img src="https://img.shields.io/badge/-4. Formatting Dates and Times %20-blue" height=40px>

### Useful ways to format [**_Date and Time_**](#-) :

```sql
-- takes 2 arguments
-- DATE_FORMAT(date value , format String)
SELECT DATE_FORMAT(NOW(), '%D %M %Y');
SELECT DATE_FORMAT(NOW(), '%d-%m-%y');

-- takes 2 arguments
-- TIME_FORMAT(date value , format String)
SELECT TIME_FORMAT(NOW(), '%H:%i %p');
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 5

<img src="https://img.shields.io/badge/-5. Calculating Dates and Times %20-blue" height=40px>

### Most useful [**_Calculations on Date and Time_**](#-) functions:

```sql
-- ADD day
SELECT DATE_ADD(NOW(), INTERVAL 1 DAY);

-- ADD year
SELECT DATE_ADD(NOW(), INTERVAL 1 YEAR);

-- ADD year from past
SELECT DATE_ADD(NOW(), INTERVAL -1 YEAR);

-- Or we can use the Function of:
SELECT DATE_SUB(NOW(), INTERVAL 1 YEAR);

-- Calc the difference between 2 dates
SELECT DATEDIFF('2019-01-05', '2019-01-01');
SELECT DATEDIFF('2019-01-05 09:00', '2019-01-01 17:00');

-- Calc the difference between 2 times
SELECT TIME_TO_SEC('09:02')- TIME_TO_SEC('09:00');
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 6

<img src="https://img.shields.io/badge/-6. IFNULL and COALESCE Functions %20-blue" height=40px>

[IFNULL()](#-) - with this function we can subtitute a null value with somethng else. </br>
[COALESCE()](#-) - with this function we supply a list of values amd this function returns the first NONE NULL value in the list </br>

### [Example IFNULL()](#-)

```sql
SELECT 
	  order_id,
    shipper_id
FROM orders;
```

![image](https://user-images.githubusercontent.com/36256986/164990324-e536e915-21fa-4d68-930b-bdf7da3a0ff8.png)


after adding the IFNULL() FUnction:

```sql
SELECT 
	  order_id,
    IFNULL(shipper_id, 'NOT assigned') AS shipper
FROM orders;
```

![image](https://user-images.githubusercontent.com/36256986/164990334-530ad370-b73b-4212-a32d-35fe8da8bcf9.png)

### [Example COALESCE()](#-)

```sql
SELECT 
	  order_id,
    shipper_id,
    comments,    
    -- If shipper_id is null & commnets also null put 'NOT assignes'
    COALESCE(shipper_id, comments, 'NOT assigned') AS shipper
FROM orders;
```

![image](https://user-images.githubusercontent.com/36256986/164990471-d89a8183-7673-472d-8b92-1ae476156332.png)

### [Excerise](#-)

Write a query t produe this result

![image](https://user-images.githubusercontent.com/36256986/164990505-eca70079-c07a-43fb-a04c-184d92a4efe3.png)

```sql
SELECT 
	  CONCAT(first_name , ' ' , last_name) AS customer,
    IFNULL(phone, 'Unknown') AS phone
FROM customers;
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 7

<img src="https://img.shields.io/badge/-7. IF Function %20-blue" height=40px>



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


