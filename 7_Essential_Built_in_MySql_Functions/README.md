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
|  3  |[Date Functions](#3)   | 
|  4  |[Formatting Dates and Times](#4)   | 
|  5  |[Calculating Dates and TImes](#5)   | 
|  6  |[The IFNULL and COALESCE Functions](#6)   | 
|  7  |[The IF Function](#7)   | 
|  8  |[The CASE Operator](#8)   | 



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

--------------------------------------------------------------------------------------------------

###### 

<img src="https://img.shields.io/badge/-X.  %20-blue" height=40px>


[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)




