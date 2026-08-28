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

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

## Create the Tables:

```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);
CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    action_date TIMESTAMP
);
```

## Create the Trigger:

```
CREATE OR REPLACE TRIGGER log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (
        :NEW.emp_id,
        :NEW.emp_name,
        :NEW.salary,
        SYSTIMESTAMP
    );
END;
/
```

## Test the Trigger:

```
INSERT INTO employees (emp_id, emp_name, salary)
VALUES (106, 'Ravi', 5000);
```

## Check the Log:

```
SELECT * FROM employee_log;
```

## OUTPUT :

<img width="723" height="611" alt="image" src="https://github.com/user-attachments/assets/8a0e0d5c-8680-446c-af59-60f8fab3c6bb" />

<img width="792" height="86" alt="image" src="https://github.com/user-attachments/assets/af56fc1d-bc2b-4b97-a9d5-27879c91c837" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

## Create the Tables:

```
CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    data VARCHAR2(100)
);
```

## Insert Sample Data

```
INSERT INTO sensitive_data VALUES (1, 'Confidential Information');
COMMIT;
```

## Create the Trigger:

```
CREATE OR REPLACE TRIGGER prevent_delete
BEFORE DELETE ON sensitive_data
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'ERROR: Deletion not allowed on this table.'
    );
END;
/
```

## Test the Trigger:

```
DELETE FROM sensitive_data
WHERE id = 1;
```

## OUTPUT:

<img width="790" height="471" alt="image" src="https://github.com/user-attachments/assets/34133df3-21a7-43b9-991e-65223e8b94e7" />

<img width="865" height="190" alt="image" src="https://github.com/user-attachments/assets/6e432c37-e931-4057-b80a-53a339d5f67f" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

## Create the Tables:

```
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);
```

## Insert Sample Data

```
INSERT INTO products
VALUES (1, 'Laptop', 50000, SYSTIMESTAMP);

COMMIT;
```

## Create the Trigger:

```
CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/
```

## Test the Trigger:

```
UPDATE products
SET price = 55000
WHERE product_id = 1;

COMMIT;
```

## Check the result:

```
SELECT product_id, product_name, price, last_modified
FROM products;
```

## OUTPUT:

<img width="700" height="582" alt="image" src="https://github.com/user-attachments/assets/2a9d2453-c0ec-4bd0-ae3a-3f8f200a0a0b" />

<img width="946" height="143" alt="image" src="https://github.com/user-attachments/assets/d39f2dea-1593-44cb-a606-c658b5bd2391" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

## Create the Tables:

```
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    order_amount NUMBER
);

CREATE TABLE audit_log (
    update_count NUMBER
);
```

## Insert Initial Data

```
INSERT INTO audit_log VALUES (0);

INSERT INTO customer_orders
VALUES (1, 'Anitha', 5000);

COMMIT;
```

## Create the Trigger:

```
CREATE OR REPLACE TRIGGER count_updates
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/
```

## Test the Trigger:

```
UPDATE customer_orders
SET order_amount = 6000
WHERE order_id = 1;

COMMIT;
```

## Check the Counter:

```
SELECT * FROM audit_log;
```

## OUTPUT:

<img width="772" height="607" alt="image" src="https://github.com/user-attachments/assets/321e3731-b815-44b8-a7ca-833bc96cf445" />

<img width="356" height="247" alt="image" src="https://github.com/user-attachments/assets/07b371d5-6819-4f66-9bb7-09a4608ba729" />

If you update the table again, the count increases:

<img width="442" height="637" alt="image" src="https://github.com/user-attachments/assets/30470967-0ca4-4c69-8f4c-416cfa0cc64c" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

## Create the Tables:

```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);
CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    action_date TIMESTAMP
);
```

## Create the Trigger:

```
CREATE OR REPLACE TRIGGER check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20002,
            'ERROR: Salary below minimum threshold.'
        );
    END IF;
END;
/
```

## Test with an Invalid Salary:

```
INSERT INTO employees
VALUES (102, 'Priya', 2500);
```

## Output:

<img width="813" height="145" alt="image" src="https://github.com/user-attachments/assets/64f4dff6-cd54-433a-9e68-30f21a70214c" />

## Test with a Valid Salary:

```
INSERT INTO employees
VALUES (103, 'Kumar', 5000);
```

## Check the Table:

```
SELECT * FROM employees;
```

## OUTPUT:

<img width="681" height="123" alt="image" src="https://github.com/user-attachments/assets/2644b44b-8a9e-4618-abd6-317509410212" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
