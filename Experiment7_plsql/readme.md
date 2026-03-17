# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

# PROGRAM 
```
DECLARE
    num1 NUMBER := 50;
    num2 NUMBER := 80;
BEGIN
    IF num1 > num2 THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
    END IF;
END;
/

```
# OUTPUT

<img width="448" height="271" alt="image" src="https://github.com/user-attachments/assets/238a8974-4180-43ba-ac4f-b0b5e9047d71" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

# PROGRAM: 
```
DECLARE
    n   NUMBER := 10;
    i   NUMBER := 1;
    sum NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
/
```
# OUTPUT:
<img width="440" height="268" alt="image" src="https://github.com/user-attachments/assets/3ca89df3-837a-47a1-b4cb-9aea574ac27f" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

# PROGRAM 
```
DECLARE
    n   NUMBER := 7;
    a   NUMBER := 0;
    b   NUMBER := 1;
    c   NUMBER;
    i   NUMBER := 3;
BEGIN
    DBMS_OUTPUT.PUT('Fibonacci sequence: ' || a || ', ' || b);

    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT(', ' || c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.NEW_LINE;
END;
/

```
# OUTPUT

<img width="424" height="250" alt="image" src="https://github.com/user-attachments/assets/0214730f-7b3c-4ab6-b292-2f2b4a6191e4" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351
# PROGRAM
```
DECLARE
    n       NUMBER := 1535;
    rem     NUMBER;
    rev     NUMBER := 0;
    temp    NUMBER;
BEGIN
    temp := n;

    WHILE temp > 0 LOOP
        rem := MOD(temp, 10);         
        rev := (rev * 10) + rem;       
        temp := FLOOR(temp / 10);      
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('n = ' || n);
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
/

```
# OUTPUT
<img width="416" height="269" alt="image" src="https://github.com/user-attachments/assets/74ba4271-8cad-4358-8528-9a48957763bc" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

# PROGRAM
```
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    IF (a > b) AND (a > c) THEN
        largest := a;
    ELSIF (b > c) THEN
        largest := b;
    ELSE
        largest := c;
    END IF;

    DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
    DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || largest);
END;
/

```
# OUTPUT

<img width="520" height="276" alt="image" src="https://github.com/user-attachments/assets/c1d8c30e-f5e2-439f-9cd6-b02c69fa1ad1" />

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

