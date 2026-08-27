# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.
```
name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
```

For example:

<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><code>select changes();</code></td>
    <td>
      <code>changes()</code><br>
      -----------------<br>
      2
    </td>
  </tr>
</table>


```sql
UPDATE suppliers
SET supplier_name=UPPER(supplier_name)
WHERE contact_person LIKE '%Singh';
```

**Output:**

<img width="1275" height="757" alt="image" src="https://github.com/user-attachments/assets/4e6743e4-5ff7-4de4-be49-7770563c835e" />

**Question 2**
---
 Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
```
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
```

For example:

<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><code>select changes();</code></td>
    <td>
      <code>changes()</code><br>
      ----------<br>
      3
    </td>
  </tr>
</table>

```sql
UPDATE sales
SET total_sell_price=quantity*sell_price
WHERE product_id=10;
```

**Output:**

<img width="1292" height="810" alt="image" src="https://github.com/user-attachments/assets/47b559a3-499f-4865-8ece-292effc004c3" />

**Question 3**
---
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table
```
---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id
```

```sql
UPDATE products
SET sell_price=sell_price*1.10
WHERE category='Bakery';
```

**Output:**

<img width="1287" height="807" alt="image" src="https://github.com/user-attachments/assets/82ab6bcb-23ae-4528-be60-00248828f161" />

**Question 4**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

For example:

<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><code>SELECT * FROM doctors;</code></td>
    <td>
      <pre>doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics</pre>
    </td>
  </tr>
</table>

```sql
DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**

<img width="1302" height="640" alt="image" src="https://github.com/user-attachments/assets/4d020aff-4440-4c22-a093-c338fcf58ae1" />

**Question 5**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

<img width="1185" height="111" alt="image" src="https://github.com/user-attachments/assets/eedda8f1-3bf8-405c-b1f3-e54aa6eabc20" />

For example:

<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><code>SELECT DISTINCT(grade) FROM customer;</code></td>
    <td>
      <pre>GRADE
----------
2
3
1
0</pre>
    </td>
  </tr>
  <tr>
    <td><code>SELECT DISTINCT(grade) FROM customer;</code></td>
    <td>
      <pre>GRADE
----------
2
3</pre>
    </td>
  </tr>
</table>

```sql
DELETE FROM customer
WHERE GRADE<2;
```

**Output:**

<img width="1321" height="757" alt="image" src="https://github.com/user-attachments/assets/f8366bb4-d283-4fed-96b2-03528d5fad9c" />

**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

Sample table: Customer

<img width="1030" height="102" alt="image" src="https://github.com/user-attachments/assets/7ffb75b4-2d6f-4c25-bf7b-bef0f4d6a188" />

For example:

<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><code>select changes();</code></td>
    <td>
      <pre>changes()
----------
14</pre>
    </td>
  </tr>
</table>

```sql
DELETE FROM customer
WHERE GRADE % 2<>0;
```

**Output:**

<img width="1317" height="680" alt="image" src="https://github.com/user-attachments/assets/da3cbd8c-893e-4f74-b6a4-8e709563a775" />

**Question 7**
---
Write a SQL query to find all employees along with the day of the week on which they were hired from the emp table

emp table
```
cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT
```

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td>
      <pre>ename       hiredate    day_of_week
----------  ----------  -----------
JONES       1981-04-02  Thursday
MARTIN      1981-09-28  Monday
BLAKE       1981-05-01  Friday
CLARK       1981-06-09  Tuesday
SCOTT       1982-12-09  Thursday
KING        1981-11-17  Tuesday
TURNER      1981-09-08  Tuesday</pre>
    </td>
  </tr>
</table>

```sql
SELECT ename,hiredate,
CASE strftime('%w',hiredate)
WHEN '0' THEN 'Sunday'
WHEN '1' THEN 'Monday'
WHEN '2' THEN 'Tuesday'
WHEN '3' THEN 'Wednesday'
WHEN '4' THEN 'Thursday'
WHEN '5' THEN 'Friday'
WHEN '6' THEN 'Saturday'
END AS day_of_week
FROM emp;
```

**Output:**

<img width="1335" height="670" alt="image" src="https://github.com/user-attachments/assets/ef6f5edc-85c4-4358-9c1a-1ec3262dd54f" />

**Question 8**
---
Write a SQL query to calculate the number of days between the hiredate and a specified date ('2024-12-31') for each employee using the JULIANDAY function from the emp table.

emp table
```
cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT
```  
For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td>
      <pre>ename       hiredate    days_worked
----------  ----------  -----------
SMITH       2024-06-02  212.0
ALLEN       2024-07-20  164.0
WARD        2024-11-02  59.0</pre>
    </td>
  </tr>
</table>

```sql
SELECT ename,hiredate,JULIANDAY('2024-12-31')-JULIANDAY(hiredate) AS days_worked
FROM emp;
```

**Output:**

<img width="1137" height="616" alt="image" src="https://github.com/user-attachments/assets/dcd36b6d-811a-404b-91ff-ee1b23b4fd67" />

**Question 9**
---
Write a SQL query to calculate the discounted price for products whose original price is between $50 and $150. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products
```
product_id | original_price | discount_percentage

 ------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 125.00 | 0.15

 103 | 200.00 | 0.20
```
For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td>
      <pre>product_id  original_price  discount_percentage  discounted_price
----------  --------------  -------------------  ----------------
101         50.0            0.1                  45.0
102         75.0            0.15                 63.75
103         100.0           0.2                  80.0</pre>
    </td>
  </tr>
</table>

```sql
SELECT product_id,original_price,discount_percentage,(original_price*(1-discount_percentage)) AS discounted_price
FROM Products
WHERE original_price BETWEEN 50 AND 150;
```

**Output:**

<img width="1322" height="570" alt="image" src="https://github.com/user-attachments/assets/a312a4b0-7f3c-44b5-ba00-9a72a5c8ac11" />

**Question 10**
---
write a SQL query to find customers who are either from the city 'New York' or who do not have a grade greater than 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```
For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td>
      <pre>customer_id  cust_name     city        grade       salesman_id
-----------  ------------  ----------  ----------  -----------
3002         Nick Rimando  Chennai     100         5001
3001         Brad Guzan    London      100         5005</pre>
    </td>
  </tr>
</table>

```sql
SELECT *
FROM customer
WHERE city='New York' OR NOT (grade>100);
```

**Output:**

<img width="1325" height="662" alt="image" src="https://github.com/user-attachments/assets/712c8846-416c-4d31-a1e3-dcc0fbea3cdd" />


## GRADE :

<img width="1463" height="787" alt="image" src="https://github.com/user-attachments/assets/7bf3d286-da01-4802-9fbc-1052ba2200bc" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
