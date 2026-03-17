# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
-- How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table
For example:

Result
Specialty          Gender    TotalDoctors
-----------------  --------  --------------
Cardiology         Male      1
Dermatology        Male      1
Gastroenterology   Female    4
Gastroenterology   Male      1
Pediatrics         Female    1
Pediatrics         Male      2
```sql
SELECT Specialty,Gender,count(*) as TotalDoctors
from Doctors
group by Specialty,Gender
order by Specialty,Gender;
```

**Output:**

![image](https://github.com/user-attachments/assets/ae1d7229-4085-4c29-8f73-88362a81eaa4)


**Question 2**
---
-- Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee
For example:

Result
city        Income
----------  ----------
Alaska      450000
Arizona     1000000
California  5300000
Florida     5350000
Georgia     250000
here

```sql
SELECT city, sum(income) as Income from employee
group by city having Income > 200000;
```

**Output:**

![image](https://github.com/user-attachments/assets/f8813709-bbe1-4c5c-9bd4-326159c3bb23)


**Question 3**
---
-- Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1



For example:

Result
occupation  MIN(workhour)
----------  -------------
Business    10
Doctor      15
Engineer    12
Teacher     9


```sql
SELECT occupation,  AVG(workhour) from employee1
group by occupation having AVG(workhour) between 10 and 12;
```

**Output:**

![image](https://github.com/user-attachments/assets/8f7a3725-509e-46fe-83d0-d03a321d1509)


**Question 4**
---
-- Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1



For example:

Result
occupation  AVG(workhour)
----------  -------------
Business    10.0
Engineer    12.0
```sql
SELECT occupation,  AVG(workhour) from employee1
group by occupation having AVG(workhour) between 10 and 12;
```

**Output:**

![image](https://github.com/user-attachments/assets/ac44350e-e9ac-4329-af5f-90e8d4b051d6)


**Question 5**
---
-- Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_name_length
---------------
10.0


```sql
SELECT avg(length(name)) as avg_name_length from customer
where city = 'Chennai';
```

**Output:**

![image](https://github.com/user-attachments/assets/405e9f2c-7a33-40cd-9750-f498c6c45f0e)


**Question 6**
---
--Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26


```sql
SELECT min(purch_amt) as MINIMUM FROM orders
order by MINIMUM ASC LIMIT 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/82129e8a-582d-4b98-9958-5d65c7982e9e)


**Question 7**
---
--Write a SQL query to find the shortest email address in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name        email           min_email_length
----------  --------------  ----------------
Ravi Kumar  ravi@gmail.com  14

```sql
SELECT name,email, length(email) as min_email_length
from customer
order by length(email) asc
limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/1713e691-de01-49fb-92fc-699eed4ac570)


**Question 8**
---
-- Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15


```sql
SELECT name as fruit_name, inventory as lowest_quantity from fruits
order by inventory asc limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/dc745da4-f1b4-4a1e-9e89-526ebc701ed4)


**Question 9**
---
-- How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table



For example:

Result
Frequency      TotalPrescriptions
-------------  ------------------
Every 3 weeks  1
Every 6 hours  1
Once           1
Once daily     4
Once daily at  1
Pending        1
Twice daily    1

```sql
SELECT Frequency,count(*) as TotalPrescriptions 
from Prescriptions
group by Frequency  
order by Frequency ;
```

**Output:**

![image](https://github.com/user-attachments/assets/ccb2c14c-76a1-4fa1-b053-69db65a07ad9)


**Question 10**
---
--Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
COUNT
----------
6

```sql
-- select count(distinct salesman_id) as COUNT
from orders;
```

**Output:**

![image](https://github.com/user-attachments/assets/96f0dce0-25a8-4f91-bd89-2376a34a4011)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
