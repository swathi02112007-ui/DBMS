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

## PL/SQL PROGRAM:

```
DECLARE
    a NUMBER := 50;
    b NUMBER := 80;
BEGIN
    IF a > b THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || a);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || b);
    END IF;
END;
```

## OUTPUT:

<img width="836" height="622" alt="image" src="https://github.com/user-attachments/assets/19382f6f-3233-44fa-a12c-9290482d0677" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

## PL/SQL PROGRAM:

```
DECLARE
    n NUMBER := 10;
    i NUMBER := 1;
    sum NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE(
        'Sum of first ' || n ||
        ' natural numbers is: ' || sum
    );
END;
/
```

## OUTPUT:

<img width="838" height="626" alt="image" src="https://github.com/user-attachments/assets/1c775526-bb96-4b1c-bf96-c61c8ba80538" />

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

## PL/SQL PROGRAM:

```
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER;
    result VARCHAR2(100) := '';
BEGIN
    result := a || ', ' || b;

    FOR i IN 3..n LOOP
        c := a + b;
        result := result || ', ' || c;

        a := b;
        b := c;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('n = ' || n);
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence: ' || result);
END;
/
```

## OUTPUT:

<img width="823" height="503" alt="image" src="https://github.com/user-attachments/assets/65bd1aff-bcca-47ce-b7c4-8aaef4c86303" />

<img width="871" height="310" alt="image" src="https://github.com/user-attachments/assets/d266c781-be81-440b-836a-ca7535a1d48f" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

## PL/SQL PROGRAM:

```
DECLARE
    n NUMBER := 1535;
    temp NUMBER;
    remainder NUMBER;
    reversed NUMBER := 0;
BEGIN
    temp := n;

    WHILE temp > 0 LOOP
        remainder := MOD(temp, 10);

        reversed := reversed * 10 + remainder;

        temp := TRUNC(temp / 10);
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('n = ' || n);
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || reversed);
END;
/
```

## OUTPUT:

<img width="842" height="513" alt="image" src="https://github.com/user-attachments/assets/5eed8a3f-1cb2-4c7e-84a2-0a9129a7bdea" />

<img width="875" height="305" alt="image" src="https://github.com/user-attachments/assets/6868c647-cc37-485c-867c-878e3276a100" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

## PL/SQL PROGRAM:

```
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
BEGIN
    DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);

    IF a >= b AND a >= c THEN
        DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || a);

    ELSIF b >= a AND b >= c THEN
        DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || b);

    ELSE
        DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || c);
    END IF;
END;
/
```

## OUTPUT:

<img width="837" height="442" alt="image" src="https://github.com/user-attachments/assets/de2e0142-b143-4e6a-926c-9f1dd9a20d27" />

<img width="870" height="295" alt="image" src="https://github.com/user-attachments/assets/3c4ae0b2-6282-46df-9b33-f0f8bb313df1" />

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
