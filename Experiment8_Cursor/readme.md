# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

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

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### CREATING TABLE :

```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER,
    dept_no NUMBER
);
```

### INSERTING VALUES :

```
INSERT INTO employees VALUES (101, 'Ravi', 'Manager', 50000, 10);
INSERT INTO employees VALUES (102, 'Priya', 'Developer', 40000, 20);
INSERT INTO employees VALUES (103, 'Arun', 'Analyst', 35000, 10);
INSERT INTO employees VALUES (104, 'Divya', 'Tester', 30000, 30);
INSERT INTO employees VALUES (105, 'Kumar', 'Developer', 45000, 20);

COMMIT;
```


### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display the employee details or an error message.

## PL/SQL PROGRAM:

```
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation
        FROM employees;

    v_emp_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || v_emp_name ||
            ', Designation: ' || v_designation
        );
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

## OUTPUT:

<img width="763" height="615" alt="Screenshot 2026-08-28 085759" src="https://github.com/user-attachments/assets/ccc93ce9-05f9-4b87-919f-6e2184f03b3b" />

<img width="772" height="166" alt="Screenshot 2026-08-28 085806" src="https://github.com/user-attachments/assets/2804f623-74f1-4f60-b875-c7b30ce13d89" />

<img width="703" height="222" alt="Screenshot 2026-08-28 085818" src="https://github.com/user-attachments/assets/b58e854c-a931-4623-91a4-d95cf8bef24f" />

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

## PL/SQL PROGRAM:

```
DECLARE
    CURSOR emp_cursor (
        min_salary NUMBER,
        max_salary NUMBER
    ) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_salary AND max_salary;

    v_count NUMBER := 0;

BEGIN
    FOR emp_rec IN emp_cursor(30000, 45000) LOOP

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Name: ' || emp_rec.emp_name ||
            ', Designation: ' || emp_rec.designation ||
            ', Salary: ' || emp_rec.salary
        );

    END LOOP;

    IF v_count = 0 THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in this salary range.');
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

## OUTPUT:

<img width="790" height="610" alt="image" src="https://github.com/user-attachments/assets/d38565ba-876f-4123-96fb-d9ec980494bf" />

<img width="723" height="197" alt="image" src="https://github.com/user-attachments/assets/42ab5b93-389e-4ba9-9670-c6a1b5a06396" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

## PL/SQL PROGRAM:

```
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, dept_no
        FROM employees;

    v_count NUMBER := 0;

BEGIN
    FOR emp_rec IN emp_cursor LOOP

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'Employee Name: ' || emp_rec.emp_name ||
            ', Department Number: ' || emp_rec.dept_no
        );

    END LOOP;

    IF v_count = 0 THEN
        DBMS_OUTPUT.PUT_LINE('No employees found.');
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

## OUTPUT:

<img width="721" height="572" alt="image" src="https://github.com/user-attachments/assets/654a0748-9a63-47c2-aec7-ad9a5d6180c5" />

<img width="722" height="208" alt="image" src="https://github.com/user-attachments/assets/05364fb9-edd5-4393-b76e-e28fecfd9e6a" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

## PL/SQL PROGRAM:

```
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, designation, salary
        FROM employees;

    emp_record emp_cursor%ROWTYPE;
    v_count NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_record;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_count := v_count + 1;

        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || emp_record.emp_id ||
            ', Name: ' || emp_record.emp_name ||
            ', Designation: ' || emp_record.designation ||
            ', Salary: ' || emp_record.salary
        );
    END LOOP;

    CLOSE emp_cursor;

    IF v_count = 0 THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

## OUTPUT:

<img width="787" height="612" alt="image" src="https://github.com/user-attachments/assets/3949d0e1-5475-439d-9cd1-f0bace341eab" />

<img width="732" height="226" alt="image" src="https://github.com/user-attachments/assets/bd44ee81-8a04-4c95-a0d9-c75e6ced940a" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

## PL/SQL PROGRAM:

```
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, salary
        FROM employees
        WHERE dept_no = 10
        FOR UPDATE;

    v_count NUMBER := 0;

BEGIN
    FOR emp_rec IN emp_cursor LOOP

        v_count := v_count + 1;

        UPDATE employees
        SET salary = salary + 5000
        WHERE CURRENT OF emp_cursor;

        DBMS_OUTPUT.PUT_LINE(
            'Salary updated for ' || emp_rec.emp_name
        );

    END LOOP;

    IF v_count = 0 THEN
        DBMS_OUTPUT.PUT_LINE(
            'No employees found in the specified department.'
        );
    ELSE
        DBMS_OUTPUT.PUT_LINE('Employee salaries updated successfully.');
    END IF;

    COMMIT;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No data found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error occurred.');
END;
/
```

## OUTPUT:

<img width="783" height="607" alt="image" src="https://github.com/user-attachments/assets/eb2aaf0b-9367-4f04-94cf-c5ae9d807a5d" />

<img width="750" height="270" alt="image" src="https://github.com/user-attachments/assets/f9ddb99a-36eb-4fa8-a260-87c8b3f44e84" />

<img width="725" height="188" alt="image" src="https://github.com/user-attachments/assets/ab6e7813-8f9f-4532-ae75-48766a24408e" />

<img width="837" height="548" alt="image" src="https://github.com/user-attachments/assets/ae17660a-7c69-4faa-bb79-ef3c66299d2a" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

