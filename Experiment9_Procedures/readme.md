# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.
# Program
```
SET SERVEROUTPUT ON;

DECLARE
    num NUMBER := 6;
    square_num NUMBER;
BEGIN
    square_num := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || square_num);
END;
/
```
**Expected Output:**  
Square of 6 is 36

<img width="894" height="236" alt="image" src="https://github.com/user-attachments/assets/d193c212-b513-4dec-ac34-2aa5a816ae96" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

# program:
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 5;
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..n LOOP
        fact := fact * i;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Factorial of ' || n || ' is ' || fact);
END;
/


```
**Expected Output:**  
Factorial of 5 is 120

<img width="439" height="73" alt="image" src="https://github.com/user-attachments/assets/5b511687-b751-4f63-b92c-382611e9c4cd" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

# program:
```
SET SERVEROUTPUT ON;

DECLARE
    num NUMBER := 12;
BEGIN
    IF MOD(num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
    END IF;
END;
/
```
**Expected Output:**  
12 is Even

<img width="249" height="68" alt="image" src="https://github.com/user-attachments/assets/5800d5aa-34e3-40fa-855a-9fdc6d11c559" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.
# program:
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 1234;
    rev NUMBER := 0;
    temp NUMBER := n;
BEGIN
    WHILE temp > 0 LOOP
        rev := rev * 10 + MOD(temp, 10);
        temp := FLOOR(temp / 10);
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Reversed number of ' || n || ' is ' || rev);
END;
/
```
**Expected Output:**  
Reversed number of 1234 is 4321

<img width="341" height="72" alt="image" src="https://github.com/user-attachments/assets/7a4567e3-6746-4c13-b6e8-3a304d6a581c" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.
# program:
```
SET SERVEROUTPUT ON;

DECLARE
    num NUMBER := 5;
BEGIN
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
    END LOOP;
END;
/
```
**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

<img width="385" height="246" alt="image" src="https://github.com/user-attachments/assets/46e03642-8300-4c52-aef0-15d71092183f" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
