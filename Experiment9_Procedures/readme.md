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

**Expected Output:**  
Square of 6 is 36

## PL/SQL PROGRAM:

```
CREATE OR REPLACE PROCEDURE find_square (
    n IN NUMBER
)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Square of ' || n || ' is ' || (n * n)
    );
END;
/
```

To call the procedure:

```
BEGIN
    find_square(6);
END;
/
```

## OUTPUT:

<img width="677" height="290" alt="image" src="https://github.com/user-attachments/assets/c5a22881-8afd-4160-a800-c74388872f82" />

<img width="705" height="330" alt="image" src="https://github.com/user-attachments/assets/d62b7f5c-98f6-4926-aadb-b04df4bc850e" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120

## PL/SQL PROGRAM:

```
CREATE OR REPLACE FUNCTION get_factorial (
    n IN NUMBER
)
RETURN NUMBER
IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..n LOOP
        fact := fact * i;
    END LOOP;

    RETURN fact;
END;
/
```

To call the function:

```
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Factorial of 5 is ' || get_factorial(5)
    );
END;
/
```

## OUTPUT:

<img width="772" height="457" alt="image" src="https://github.com/user-attachments/assets/10e9548d-44f4-4496-9613-2998aadff02f" />

<img width="733" height="350" alt="image" src="https://github.com/user-attachments/assets/9536f257-4b0e-40b0-a1a6-4d7e88c7fe7a" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even

## PL/SQL PROGRAM:

```
CREATE OR REPLACE PROCEDURE check_even_odd (
    n IN NUMBER
)
IS
BEGIN
    IF MOD(n, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(n || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
    END IF;
END;
/
```

To call the procedure:

```
BEGIN
    check_even_odd(12);
END;
/
```

## OUTPUT:

<img width="738" height="402" alt="image" src="https://github.com/user-attachments/assets/cac717a8-a6d9-4672-8cea-c3c498919da4" />

<img width="705" height="330" alt="image" src="https://github.com/user-attachments/assets/cdec11c3-4ff5-4371-857b-e2bf1b4e8201" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

## PL/SQL PROGRAM:

```
CREATE OR REPLACE FUNCTION reverse_number (
    n IN NUMBER
)
RETURN NUMBER
IS
    temp NUMBER := n;
    remainder NUMBER;
    reversed NUMBER := 0;
BEGIN
    WHILE temp > 0 LOOP
        remainder := MOD(temp, 10);
        reversed := reversed * 10 + remainder;
        temp := TRUNC(temp / 10);
    END LOOP;

    RETURN reversed;
END;
/
```

To call the function:

```
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Reversed number of 1234 is ' ||
        reverse_number(1234)
    );
END;
/
```

## OUTPUT:

<img width="772" height="538" alt="image" src="https://github.com/user-attachments/assets/735b3ba7-1161-485f-ba8d-ff3c3266bba0" />

<img width="722" height="361" alt="image" src="https://github.com/user-attachments/assets/bc01b2ff-f65c-4b6f-b46a-91ef0b9bd5de" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

## PL/SQL PROGRAM:

```
CREATE OR REPLACE PROCEDURE print_table (
    n IN NUMBER
)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE(
        'Multiplication table of ' || n || ':'
    );

    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(
            n || ' x ' || i || ' = ' || (n * i)
        );
    END LOOP;
END;
/
```

To call the procedure:

```
BEGIN
    print_table(5);
END;
/
```

## OUTPUT:

<img width="726" height="445" alt="image" src="https://github.com/user-attachments/assets/60fafcc3-21e1-4c37-9782-a12506704362" />

<img width="657" height="390" alt="image" src="https://github.com/user-attachments/assets/f9198ea3-c71e-4fdf-8e26-08d5709dac13" />

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
