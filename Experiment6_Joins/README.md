# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**

<img width="1475" height="805" alt="image" src="https://github.com/user-attachments/assets/029fbc28-b24d-4c24-a162-d433bc04d661" />


```
SELECT p.first_name, s.*
FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id
WHERE p.discharge_date BETWEEN '2024-03-01' AND '2024-03-31'
  AND NOT (p.admission_date BETWEEN '2024-03-01' AND '2024-03-31');

```

**Output:**

<img width="1263" height="514" alt="image" src="https://github.com/user-attachments/assets/77267e97-e7f2-4cca-a525-bcdd5fca13d3" />


**Question 2**
<img width="1432" height="854" alt="image" src="https://github.com/user-attachments/assets/87d7760b-f70a-440a-9342-e30a535e7ee3" />


```
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.commission
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;

```

**Output:**

<img width="1313" height="841" alt="image" src="https://github.com/user-attachments/assets/26b547bb-630f-4b3e-8b48-fb7cf655b322" />

**Question 3**

<img width="1491" height="850" alt="image" src="https://github.com/user-attachments/assets/959d46e5-1e79-44f4-adc8-cca228d1987b" />


```
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.commission
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id;

```

**Output:**

<img width="1286" height="843" alt="image" src="https://github.com/user-attachments/assets/41823c08-82cd-49c2-97b4-91cac611728d" />


**Question 4**

<img width="1426" height="577" alt="image" src="https://github.com/user-attachments/assets/f1816348-6dff-4620-9da1-6cebdb085927" />


```
SELECT 
    s.name AS salesman_name,
    c.cust_name AS customer_name
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id;

```

**Output:**

<img width="848" height="837" alt="image" src="https://github.com/user-attachments/assets/92fe8183-4793-43ba-88df-5cb8655af151" />


**Question 5**

<img width="1454" height="795" alt="image" src="https://github.com/user-attachments/assets/32d12918-538a-460a-aecd-15372077a434" />


```
SELECT 
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

<img width="1266" height="562" alt="image" src="https://github.com/user-attachments/assets/8f6a0010-5e62-4656-adc0-4afbfdf2bdf2" />


**Question 6**

<img width="1459" height="481" alt="image" src="https://github.com/user-attachments/assets/b9698922-bf5d-46b0-b0e4-0d653014a299" />


```
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE c.city = 'London';

```

**Output:**

<img width="1293" height="571" alt="image" src="https://github.com/user-attachments/assets/5d46aaa9-cd3a-47c7-ba73-cdc35ff72103" />


**Question 7**
<img width="1460" height="848" alt="image" src="https://github.com/user-attachments/assets/8fec8b00-eda9-42c1-a77e-5e362f7674ba" />


```
SELECT 
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
JOIN salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1278" height="838" alt="image" src="https://github.com/user-attachments/assets/7f0dba00-dd97-4905-85dd-3d2cb7d219e3" />


**Question 8**
<img width="1448" height="747" alt="image" src="https://github.com/user-attachments/assets/84451c09-4f29-46cd-a3e0-99677ab73b3a" />


```
SELECT 
    p.first_name AS patient_name,
    t.result_id,
    t.patient_id,
    t.test_name,
    t.result,
    t.test_date
FROM patients p
JOIN test_results t ON p.patient_id = t.patient_id
WHERE t.test_name = 'Blood Pressure';

```

**Output:**

<img width="1290" height="496" alt="image" src="https://github.com/user-attachments/assets/487699b4-cb85-4363-b07d-1ef53a178ef9" />


**Question 9**

<img width="1458" height="837" alt="image" src="https://github.com/user-attachments/assets/2ede3bed-f6af-4430-ac52-8a7d6676a2e2" />


```
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;

```

**Output:**

<img width="1270" height="835" alt="image" src="https://github.com/user-attachments/assets/ceafe18c-b958-4944-a21f-521519d23dfc" />


**Question 10**

<img width="1465" height="809" alt="image" src="https://github.com/user-attachments/assets/54969564-4a2a-489f-9590-a1881eb22b97" />


```
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM patients p
INNER JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NOT NULL;

```

**Output:**

<img width="1264" height="493" alt="image" src="https://github.com/user-attachments/assets/389c35f9-344e-402a-a1d9-5cacc54fc410" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
