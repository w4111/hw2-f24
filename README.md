# Homework 2

* Assigned: 9/26
* Due: 10/3 11:59PM (No grace days/late submissions accepted at all beyond 10/7 11:59 PM EST)
* Worth 3.75% of your grade
* Done and submitted individually (as with all the homeworks) **via [Gradescope](https://www.gradescope.com)**


## Submission

You will submit all your work on Gradescope. You will upload screenshots and / or type in your solution directly corresponding to each question for Q1-4. You're encouraged to show your working process / intermediate steps for partial mark considerations, but please clearly indicate your final answer. 
You will submit a single file of your jupyter notebook for Q5.

## 1. Relational Algebra

**(2 point each, 12 points total)**

T1

|A | B | C |
|---|---|---|
|1 | x | a |
|2 | y | c |
|2 | y | b |
|2 | z | c |


T2

B | C | D
---|---|---
1 | x | c
2 | y | c
3 | x | a


Write the result table for the relational algebra expressions given T1 and T2.

Note: We assume the attributes whose values are all numbers are the same type (integers),
and all the letters are the same type (char). If the result table is empty, write the schema of the table.


1. π<sub>A,B</sub>(T1)

2. T1 × π<sub>A</sub>(T1)

3. T1 ⨝<sub>T1.B=T2.C</sub> T2

4. (T1 ∪ T2) − (T1 ∩ T2)

5. T1 ⨝<sub>T1.A&gt;T2.B</sub> (σ<sub>B&ne;2</sub>(T2))

6. T1 ⨝<sub>T1.A&gt;R.A</sub> p(R(1->A, 2->D), π<sub>B, C</sub>(T2))

## 2. More Relational Algebra

**(2 points each, 7 points total)**

Consider the simplified Employee Stock Ownership Database below (primary keys are in **bold**):

* Person(**ssn**, companyid, salary)

This is an employee table. *companyid* is a foreign key which points to *Company*.
We assume one employee can only work at one company. 

* Supervision(**employeeid**, **managerid**)

This table describes how supervisor relationships between employees. Both *employeeid* 
and *managerid* are foreign keys that point to *Person*

* Company(**companyid**, companyname, location)

* Holding(**ssn**, **companyid**, sharenum)

Holding table describes an employee(*ssn*) owns *sharenum* stocks of *companyid*.

Construct relational algebra for the following queries:
   
* **Q1**: (2 points) Find the *ssn* of the persons who owns stocks at companies where he/she has not worked for.

* **Q2**: (2 points) Find the *ssn* of the persons who owns more *sharenum* of a stock than all of his/her manager owns.
    (Note: Each *companyid* represents a different stock).

* **Q3**: (3 points) Find the *ssn* of the persons who own three different stocks where the *sharenum* of one stock is 
    larger than the sum of *sharenum* of the other two stocks.
    (Note: the total number of stocks qualified persons own could be more than 3)


## 3. Relational Algebra -> SQL

**(3 points each, 6 points total)**

Here are two relations, (primary keys are in **bold**):

* Goods(**gid**, g_name, price)

* Supply(**supplyid**, **gid**, cost)

For each of the following relational algebra expressions, first describe its meaning. Second, translate the expression to SQL. Make sure your SQL can be executed in Postgres.

First, describe the meaning of following relational algebra expressions in one or two sentences.
Second, translate the following relational algebra expressions in SQL. Make sure your SQL can be executed.

1. π<sub>g_name</sub>(σ<sub>price &lt; cost</sub>(π<sub>g_name, price, cost</sub>(Goods ⨝ Supply)))

**Optional question for extra credit. (2 points)**

2. π<sub>supplyid</sub>(Supply/π<sub>gid</sub>(σ<sub>supplyid='1096'</sub>(Supply)))


  The textbook defines division as following:
   
   <img width="479" alt="division-defition" src="https://github.com/user-attachments/assets/7e97fa52-d818-4d7c-97aa-a6ca2b476ff5">

3. (3 points)
   
   p(S1, Goods ⨝ Supply)
   p(S2, Goods ⨝ Supply)
   π<sub>S1.supplyid</sub>(S1 ⨝<sub>S1.supplyid = S2.supplyid, S1.gid ≠ S2.gid, S1.price = S2.price</sub> S2)
   (Note: You only need to describe the meaning of the last expression)
   



## 4. English Description -> SQL

**(2 points each, 6 points total)**

Write SQL queries for the following English descriptions using the same relationships in Q3:
1. Find the total price of goods if all supplies are sold.
2. Create a table *Supcount* by finding the total number of suppliers providing each good. The *Supcount* table shall contain two columns (gid, c)
3. Use only the *Supcount* table you created and the Goods table to compute the total price of goods if all suppliers are sold.


## 5. More SQL
**(12 points total)**
* [Click here to open the HW2 notebook in google colab](https://drive.google.com/file/d/1m4w2Qw1aoqx4ePyBl6NZDD8TWHnu1Qww/view?usp=sharing)
* Click "ctrl + s" and save a copy to your own Google Drive
* Or download the Jupyter notebook in the repo
* Follow the instructions in the notebook to complete and submit
