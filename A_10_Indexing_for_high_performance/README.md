###### _

<img src="https://img.shields.io/badge/-10. Indexing for high performance %20-blue" height=60px>


|     |  Subject           |		|
|:---:|:------------------------------|:----------|  
|     |[Introduction](#Introduction)   |             
|  1  |[Creating Stored Pocedure](#Creating_Stored_Pocedure)   |             
|  2  |[Dropping Stored Pocedure](#Dropping_Stored_Pocedure)   |
|  3  |[Parameters](#Parameters)   | 
|  4  |[Parameters with default values](#Parameters_with_default_values)   | 
|  5  |[Parameters validation](#Parameters_validation)   | 
|  6  |[Procedure Return OUT Parameters](#Procedure_Return_OUT_Parameters)   | 
|  7  |[Variables](#Variables)   | 
|  8  |[Functions](#Functions)   | 
|  9  |[9](#9)   | 


--------------------------------------------------------------------------------------------------

###### Introduction

<img src="https://img.shields.io/badge/-Introduction  %20-blue" height=40px>

[Indexes](#-) speed up our queries dramatically.</br>
[Indexes](#-) are basically data structures , that Database engine use to quickly find data.</br>

### Cost of [Indexes](#-)

1. [Increase DB](#-) - They increase the size of our DB, because they have to permenently stored next to our tables.
2. [Slow down the writes](#-) - every time we ADD, UPDATE, DELETE a record , MySql has to update the corresponding [INDEXES](#-) . this will impact the perfromance of our right operations.

We should reserve [Indexes](#-) for performance critical queries. </br>
One of the common mistakes developers do is that they add [Indexes](#-) at the time of designing thier tables.</br>
We don't create [Indexes](#-) based on our tables.</br>
We create [Indexes](#-) based on our queries.</br>

Because the whole point of [Indexes](#-) is to speed up a Slow Query.

* Internally, [Indexes](#-) are often stored as BIANTRY tree

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
