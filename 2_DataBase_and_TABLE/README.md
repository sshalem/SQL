###### _
<img src="https://img.shields.io/badge/-2_DataBase_and_TABLE %20-blue" height=60px>

|     |  Subject           |          |
|:---:|:------------------------------|:-------| 
|  1  |[CREATE DATABASE](#1)   | 
|  2  |[USE keyword](#2)       | 
|  3  |[CREATE TABLE](#3)      | 
|     |                        |  [TABLE constraints](#3-1)  |
|  4  |[DESCRIBE command](#4)  |  
|  5  |[DROP (delete)](#-5)    | 
|  6  |[ALTER TABLE … ADD/DROP](#-6)    | 
|  7  |[](#-7)    | 


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

<img src="https://img.shields.io/badge/-7. %20-blue" height=40px>

```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 8

<img src="https://img.shields.io/badge/-8. %20-blue" height=40px>

```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 9

<img src="https://img.shields.io/badge/-9. %20-blue" height=40px>

```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)

--------------------------------------------------------------------------------------------------

###### 10

<img src="https://img.shields.io/badge/-10. %20-blue" height=40px>

```sql
```

[<img src="https://img.shields.io/badge/-Back to top%20-brown" height=22px>](#_)
