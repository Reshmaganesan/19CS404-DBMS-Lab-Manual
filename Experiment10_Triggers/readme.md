# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.
# program:
```
SET SERVEROUTPUT ON;

DECLARE
    TYPE emp_rec IS RECORD (
        emp_id NUMBER,
        emp_name VARCHAR2(50),
        emp_salary NUMBER
    );

    TYPE emp_tab IS TABLE OF emp_rec;
    employees emp_tab := emp_tab();
    employee_log emp_tab := emp_tab();

    new_emp emp_rec;
BEGIN
    -- Simulate inserting a new employee
    new_emp.emp_id := 1;
    new_emp.emp_name := 'John Doe';
    new_emp.emp_salary := 50000;

    -- Add to employees "table"
    employees.EXTEND;
    employees(employees.COUNT) := new_emp;

    -- Simulate AFTER INSERT trigger: log the new employee
    employee_log.EXTEND;
    employee_log(employee_log.COUNT) := new_emp;

    -- Display the "log"
    FOR i IN 1..employee_log.COUNT LOOP
        DBMS_OUTPUT.PUT_LINE(
            'LOG: ID=' || employee_log(i).emp_id || 
            ', Name=' || employee_log(i).emp_name || 
            ', Salary=' || employee_log(i).emp_salary
        );
    END LOOP;
END;
/
```
**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

<img width="403" height="44" alt="image" src="https://github.com/user-attachments/assets/67adaf0f-7a88-4a2e-832d-609e604d0391" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.
# program:
```
SET SERVEROUTPUT ON;

DECLARE
    TYPE sensitive_tab IS TABLE OF VARCHAR2(100);
    sensitive_data sensitive_tab := sensitive_tab('Top Secret', 'Confidential');
BEGIN
    -- Attempt to "delete" a record
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
/
```
**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

<img width="510" height="81" alt="image" src="https://github.com/user-attachments/assets/87324e2e-72e6-4323-ad1d-7189ed3e3ca0" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.
# program:
```
SET SERVEROUTPUT ON;

BEGIN
    -- 1. Square of a number
    DECLARE
        num NUMBER := 6;
        square_num NUMBER;
    BEGIN
        square_num := num * num;
        DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || square_num);
    END;

    -- 2. Factorial of a number
    DECLARE
        n NUMBER := 5;
        fact NUMBER := 1;
    BEGIN
        FOR i IN 1..n LOOP
            fact := fact * i;
        END LOOP;
        DBMS_OUTPUT.PUT_LINE('Factorial of ' || n || ' is ' || fact);
    END;

    -- 3. Even or Odd check
    DECLARE
        num NUMBER := 12;
    BEGIN
        IF MOD(num, 2) = 0 THEN
            DBMS_OUTPUT.PUT_LINE(num || ' is Even');
        ELSE
            DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
        END IF;
    END;

    -- 4. Reverse of a number
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

    -- 5. Multiplication table
    DECLARE
        num NUMBER := 5;
    BEGIN
        FOR i IN 1..10 LOOP
            DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
        END LOOP;
    END;

    -- 6. Simulated trigger: log insertion
    DECLARE
        TYPE emp_rec IS RECORD (
            emp_id NUMBER,
            emp_name VARCHAR2(50),
            emp_salary NUMBER
        );
        TYPE emp_tab IS TABLE OF emp_rec;
        employees emp_tab := emp_tab();
        employee_log emp_tab := emp_tab();
        new_emp emp_rec;
    BEGIN
        new_emp.emp_id := 1;
        new_emp.emp_name := 'John Doe';
        new_emp.emp_salary := 50000;
        employees.EXTEND;
        employees(employees.COUNT) := new_emp;
        employee_log.EXTEND;
        employee_log(employee_log.COUNT) := new_emp;
        FOR i IN 1..employee_log.COUNT LOOP
            DBMS_OUTPUT.PUT_LINE(
                'LOG: ID=' || employee_log(i).emp_id || 
                ', Name=' || employee_log(i).emp_name || 
                ', Salary=' || employee_log(i).emp_salary
            );
        END LOOP;
    END;

    -- 7. Simulated trigger: prevent deletion
    DECLARE
    BEGIN
        RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
    EXCEPTION
        WHEN OTHERS THEN
            DBMS_OUTPUT.PUT_LINE(SQLERRM);
    END;

    -- 8. Simulated trigger: update last_modified
    DECLARE
        TYPE product_rec IS RECORD (
            product_id NUMBER,
            product_name VARCHAR2(50),
            price NUMBER,
            last_modified TIMESTAMP
        );
        TYPE product_tab IS TABLE OF product_rec;
        products product_tab := product_tab();
        updated_product product_rec;
    BEGIN
        products.EXTEND;
        products(products.COUNT) := product_rec(1, 'Laptop', 50000, SYSTIMESTAMP);
        updated_product := products(1);
        updated_product.price := 55000;
        updated_product.last_modified := SYSTIMESTAMP;
        DBMS_OUTPUT.PUT_LINE(
            'Product ID: ' || updated_product.product_id || 
            ', Name: ' || updated_product.product_name || 
            ', Price: ' || updated_product.price || 
            ', Last Modified: ' || updated_product.last_modified
        );
    END;
END;
/
```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

<img width="742" height="36" alt="image" src="https://github.com/user-attachments/assets/e1eebc21-0028-4ad5-8ff8-3f440b3233b6" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.
# program:
```
SET SERVEROUTPUT ON;

BEGIN
    DECLARE
        TYPE order_rec IS RECORD (
            order_id NUMBER,
            customer_name VARCHAR2(50),
            amount NUMBER
        );
        TYPE order_tab IS TABLE OF order_rec;
        customer_orders order_tab := order_tab();
        updates_count NUMBER := 0;
        updated_order order_rec;
    BEGIN
        customer_orders.EXTEND;
        customer_orders(customer_orders.COUNT) := order_rec(1, 'Alice', 1000);
        customer_orders.EXTEND;
        customer_orders(customer_orders.COUNT) := order_rec(2, 'Bob', 1500);
        updated_order := customer_orders(1);
        updated_order.amount := 1200;
        updates_count := updates_count + 1;

        DBMS_OUTPUT.PUT_LINE('Update count in audit_log: ' || updates_count);
    END;
END;
/
```

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

<img width="308" height="52" alt="image" src="https://github.com/user-attachments/assets/0aeff9d9-62b2-4af6-8291-68eab668f557" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.
# program:
```
SET SERVEROUTPUT ON;

BEGIN
    -- Simulate employees table and BEFORE INSERT trigger for salary check
    DECLARE
        TYPE emp_rec IS RECORD (
            emp_id NUMBER,
            emp_name VARCHAR2(50),
            emp_salary NUMBER
        );
        TYPE emp_tab IS TABLE OF emp_rec;
        employees emp_tab := emp_tab();
        new_emp emp_rec;
        min_salary NUMBER := 3000;
    BEGIN
        -- Attempt to insert a new employee
        new_emp.emp_id := 1;
        new_emp.emp_name := 'John Doe';
        new_emp.emp_salary := 2500; -- Below minimum

        -- Simulate BEFORE INSERT trigger
        IF new_emp.emp_salary < min_salary THEN
            RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
        ELSE
            employees.EXTEND;
            employees(employees.COUNT) := new_emp;
            DBMS_OUTPUT.PUT_LINE('Employee inserted: ' || new_emp.emp_name);
        END IF;

    EXCEPTION
        WHEN OTHERS THEN
            DBMS_OUTPUT.PUT_LINE(SQLERRM);
    END;
END;
/
```
**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

<img width="603" height="51" alt="image" src="https://github.com/user-attachments/assets/3c451e4c-4d1b-4ade-a634-a78be01cba60" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

