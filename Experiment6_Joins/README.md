## Experiment 6: Joins

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
--
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Salesman</th>
    <th>Cust_name</th>
    <th>City</th>
  </tr>
  <tr>
    <td>Bob Emily</td>
    <td>Brad Davis</td>
    <td>New York</td>
  </tr>
  <tr>
    <td>Nail Knite</td>
    <td>Fabian Johns</td>
    <td>Paris</td>
  </tr>
  <tr>
    <td>Pit Alex</td>
    <td>Brad Guzan</td>
    <td>London</td>
  </tr>
  <tr>
    <td>Pit Alex</td>
    <td>Julian Green</td>
    <td>London</td>
  </tr>
  <tr>
    <td>Mc Lyon</td>
    <td>Fabian Johns</td>
    <td>Paris</td>
  </tr>
</table>

```sql
SELECT a.name AS Salesman, b.cust_name, a.city FROM salesman a, customer b WHERE a.city = b.city;
```

**Output:**

<img width="1004" height="861" alt="image" src="https://github.com/user-attachments/assets/6de7de7e-ca52-4a81-9409-9b66efcc337a" />

**Question 2**
---
Write an SQL query to select all columns from the 'customer' table (aliased as 'c') by performing a LEFT JOIN with the 'orders' table on the 'customer_id' column, including only those orders where the order date falls between '2012-08-01' and '2012-08-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Customer ID</th>
    <th>Cust_name</th>
    <th>City</th>
    <th>Grade</th>
    <th>Salesman ID</th>
  </tr>
  <tr>
    <td>3009</td>
    <td>Geoff Cameron</td>
    <td>Berlin</td>
    <td>100</td>
    <td>5003</td>
  </tr>
  <tr>
    <td>3003</td>
    <td>Jozy Altidore</td>
    <td>Moscow</td>
    <td>200</td>
    <td>5007</td>
  </tr>
</table>

```sql
SELECT c.*
FROM customer AS c
LEFT JOIN orders AS o
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-08-01' AND '2012-08-30';
```

**Output:**

<img width="1400" height="839" alt="image" src="https://github.com/user-attachments/assets/e0bc4122-df00-4ed9-88cb-aeb8b78f5dc8" />

**Question 3**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Salesman Name</th>
    <th>Customer Name</th>
  </tr>
  <tr>
    <td>Bob Emily</td>
    <td>Brad Davis</td>
  </tr>
  <tr>
    <td>Bob Emily</td>
    <td>Nick Rimando</td>
  </tr>
  <tr>
    <td>Nail Knite</td>
    <td>Graham Zusi</td>
  </tr>
  <tr>
    <td>Nail Knite</td>
    <td>Julian Green</td>
  </tr>
  <tr>
    <td>Pit Alex</td>
    <td>Brad Guzan</td>
  </tr>
  <tr>
    <td>Mc Lyon</td>
    <td>Fabian Johns</td>
  </tr>
  <tr>
    <td>Paul Adam</td>
    <td>Jozy Altidore</td>
  </tr>
  <tr>
    <td>Lauson Hen</td>
    <td>Geoff Cameron</td>
  </tr>
</table>

```sql
SELECT a.name AS salesman_name, b.cust_name AS customer_name FROM salesman a LEFT JOIN customer b ON a.salesman_id = b.salesman_id;
```

**Output:**

<img width="1259" height="869" alt="image" src="https://github.com/user-attachments/assets/ef27597b-8ba7-4efa-a0c1-c42092dac1dd" />

**Question 4**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

PATIENTS TABLE:
```
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT
```

DOCTORS TABLE:

```
name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)
```

For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Patient Name</th>
    <th>Doctor Name</th>
  </tr>
  <tr>
    <td>Bob</td>
    <td>Emily</td>
  </tr>
</table>

```sql
SELECT p.first_name AS patient_name, d.first_name AS doctor_name 
FROM patients p 
JOIN doctors d ON p.doctor_id = d.doctor_id 
WHERE p.discharge_date IS NOT NULL;
```

**Output:**

<img width="956" height="857" alt="image" src="https://github.com/user-attachments/assets/3df739ec-67c6-4df9-bf1a-21a73aa45eb6" />

**Question 5**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Customer Name</th>
    <th>City</th>
    <th>Salesman</th>
    <th>Commission</th>
  </tr>
  <tr>
    <td>Nick Rimando</td>
    <td>Chennai</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>Graham Zusi</td>
    <td>California</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>Brad Guzan</td>
    <td>London</td>
    <td>Pit Alex</td>
    <td>0.11</td>
  </tr>
  <tr>
    <td>Fabian Johns</td>
    <td>Paris</td>
    <td>Mc Lyon</td>
    <td>0.14</td>
  </tr>
  <tr>
    <td>Brad Davis</td>
    <td>New York</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>Geoff Cameron</td>
    <td>Berlin</td>
    <td>Lauson Hen</td>
    <td>0.12</td>
  </tr>
  <tr>
    <td>Julian Green</td>
    <td>London</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>Jozy Altidore</td>
    <td>Moscow</td>
    <td>Paul Adam</td>
    <td>0.13</td>
  </tr>
</table>

```sql
SELECT c.cust_name AS "Customer Name", c.city, s.name AS "Salesman", s.commission 
FROM customer c 
JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1274" height="870" alt="image" src="https://github.com/user-attachments/assets/4c795bcf-9c4f-4ba2-9ab8-26f79a8bdb48" />

**Question 6**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders
```
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```
Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
For example:

**<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Ord No</th>
    <th>Ord Date</th>
    <th>Purch Amt</th>
    <th>Customer Name</th>
    <th>Grade</th>
    <th>Salesman</th>
    <th>Commission</th>
  </tr>
  <tr>
    <td>70001</td>
    <td>2012-10-05</td>
    <td>150.5</td>
    <td>Graham Zusi</td>
    <td>200</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>70009</td>
    <td>2012-09-10</td>
    <td>270.65</td>
    <td>Brad Guzan</td>
    <td>100</td>
    <td>Pit Alex</td>
    <td>0.11</td>
  </tr>
  <tr>
    <td>70002</td>
    <td>2012-10-05</td>
    <td>65.26</td>
    <td>Nick Rimando</td>
    <td>100</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>70004</td>
    <td>2012-08-17</td>
    <td>110.5</td>
    <td>Geoff Cameron</td>
    <td>100</td>
    <td>Lauson Hen</td>
    <td>0.12</td>
  </tr>
  <tr>
    <td>70007</td>
    <td>2012-09-10</td>
    <td>948.5</td>
    <td>Graham Zusi</td>
    <td>200</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>70005</td>
    <td>2012-07-27</td>
    <td>2400.6</td>
    <td>Brad Davis</td>
    <td>200</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>70008</td>
    <td>2012-09-10</td>
    <td>5760.0</td>
    <td>Nick Rimando</td>
    <td>100</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>70010</td>
    <td>2012-10-10</td>
    <td>1983.43</td>
    <td>Fabian Johns</td>
    <td>300</td>
    <td>Mc Lyon</td>
    <td>0.14</td>
  </tr>
  <tr>
    <td>70003</td>
    <td>2012-10-10</td>
    <td>2480.4</td>
    <td>Geoff Cameron</td>
    <td>100</td>
    <td>Lauson Hen</td>
    <td>0.12</td>
  </tr>
  <tr>
    <td>70012</td>
    <td>2012-06-27</td>
    <td>250.45</td>
    <td>Julian Green</td>
    <td>300</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>70011</td>
    <td>2012-08-17</td>
    <td>75.29</td>
    <td>Jozy Altidore</td>
    <td>200</td>
    <td>Paul Adam</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>70013</td>
    <td>2012-04-25</td>
    <td>3045.6</td>
    <td>Nick Rimando</td>
    <td>100</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
</table>**

```sql
SELECT a.ord_no, a.ord_date, a.purch_amt, b.cust_name AS "Customer Name", b.grade, c.name AS "Salesman", c.commission 
FROM orders a 
JOIN customer b ON a.customer_id = b.customer_id 
JOIN salesman c ON a.salesman_id = c.salesman_id;
```

**Output:**

<img width="1345" height="667" alt="image" src="https://github.com/user-attachments/assets/f3754f00-771d-46c9-9366-5eb4e0b0e34b" />

**Question 7**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Customer Name</th>
    <th>Customer City</th>
    <th>Grade</th>
    <th>Salesman</th>
    <th>Salesman City</th>
  </tr>
  <tr>
    <td>Brad Guzan</td>
    <td>London</td>
    <td>100</td>
    <td>Pit Alex</td>
    <td>London</td>
  </tr>
  <tr>
    <td>Nick Rimando</td>
    <td>Chennai</td>
    <td>100</td>
    <td>Bob Emily</td>
    <td>New York</td>
  </tr>
  <tr>
    <td>Jozy Altidore</td>
    <td>Moscow</td>
    <td>200</td>
    <td>Paul Adam</td>
    <td>Rome</td>
  </tr>
  <tr>
    <td>Graham Zusi</td>
    <td>California</td>
    <td>200</td>
    <td>Nail Knite</td>
    <td>Paris</td>
  </tr>
  <tr>
    <td>Brad Davis</td>
    <td>New York</td>
    <td>200</td>
    <td>Bob Emily</td>
    <td>New York</td>
  </tr>
  <tr>
    <td>Geoff Cameron</td>
    <td>Berlin</td>
    <td>100</td>
    <td>Lauson Hen</td>
    <td>San Jose</td>
  </tr>
</table>

```sql
SELECT a.cust_name, a.city, a.grade, b.name AS "Salesman", b.city AS "city" 
FROM customer a 
JOIN salesman b ON a.salesman_id = b.salesman_id 
WHERE a.grade < 300 
ORDER BY a.customer_id ASC;
```

**Output:**

<img width="1200" height="801" alt="image" src="https://github.com/user-attachments/assets/0e9757ed-f657-459b-a7e5-2b398185e1f7" />

**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/022afd87-4918-4c7b-b15d-06418ce0f483" />

TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date

<img width="1060" height="171" alt="image" src="https://github.com/user-attachments/assets/42e727c5-e874-4d7c-9633-0015c668d220" />

For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Patient ID</th>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Date of Birth</th>
    <th>Admission Date</th>
    <th>Discharge Date</th>
    <th>Doctor ID</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Alice</td>
    <td>Williams</td>
    <td>1980-05-12</td>
    <td>2024-01-10</td>
    <td>NULL</td>
    <td>1</td>
  </tr>
</table>

```sql
SELECT p.* 
FROM patients p 
JOIN test_results t ON p.patient_id = t.patient_id 
WHERE t.test_name IN ('Blood Test', 'Blood Pressure') 
  AND t.result NOT LIKE '%Normal%';
```

**Output:**

<img width="1334" height="805" alt="image" src="https://github.com/user-attachments/assets/e20abcd2-e00f-4d57-aa24-db2ee1f7d4b9" />

**Question 9**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer
```
 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
```
Sample table: orders
```
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
```
Sample table: salesman
```
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
```
For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Customer Name</th>
    <th>City</th>
    <th>Order No</th>
    <th>Order Date</th>
    <th>Order Amount</th>
    <th>Salesman</th>
    <th>Commission</th>
  </tr>
  <tr>
    <td>Nick Rimando</td>
    <td>Chennai</td>
    <td>70002</td>
    <td>2012-10-05</td>
    <td>65.26</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>Nick Rimando</td>
    <td>Chennai</td>
    <td>70008</td>
    <td>2012-09-10</td>
    <td>5760.0</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>Nick Rimando</td>
    <td>Chennai</td>
    <td>70013</td>
    <td>2012-04-25</td>
    <td>3045.6</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>Graham Zusi</td>
    <td>California</td>
    <td>70001</td>
    <td>2012-10-05</td>
    <td>150.5</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>Graham Zusi</td>
    <td>California</td>
    <td>70007</td>
    <td>2012-09-10</td>
    <td>948.5</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>Brad Guzan</td>
    <td>London</td>
    <td>70009</td>
    <td>2012-09-10</td>
    <td>270.65</td>
    <td>Pit Alex</td>
    <td>0.11</td>
  </tr>
  <tr>
    <td>Fabian Johns</td>
    <td>Paris</td>
    <td>70010</td>
    <td>2012-10-10</td>
    <td>1983.43</td>
    <td>Mc Lyon</td>
    <td>0.14</td>
  </tr>
  <tr>
    <td>Brad Davis</td>
    <td>New York</td>
    <td>70005</td>
    <td>2012-07-27</td>
    <td>2400.6</td>
    <td>Bob Emily</td>
    <td>0.15</td>
  </tr>
  <tr>
    <td>Geoff Cameron</td>
    <td>Berlin</td>
    <td>70003</td>
    <td>2012-10-10</td>
    <td>2480.4</td>
    <td>Lauson Hen</td>
    <td>0.12</td>
  </tr>
  <tr>
    <td>Geoff Cameron</td>
    <td>Berlin</td>
    <td>70004</td>
    <td>2012-08-17</td>
    <td>110.5</td>
    <td>Lauson Hen</td>
    <td>0.12</td>
  </tr>
  <tr>
    <td>Julian Green</td>
    <td>London</td>
    <td>70012</td>
    <td>2012-06-27</td>
    <td>250.45</td>
    <td>Nail Knite</td>
    <td>0.13</td>
  </tr>
  <tr>
    <td>Jozy Altidore</td>
    <td>Moscow</td>
    <td>70011</td>
    <td>2012-08-17</td>
    <td>75.29</td>
    <td>Paul Adam</td>
    <td>0.13</td>
  </tr>
</table>

```sql
SELECT a.cust_name, a.city, b.ord_no, b.ord_date, b.purch_amt AS "Order Amount", c.name, c.commission 
FROM customer a 
LEFT JOIN orders b ON a.customer_id = b.customer_id 
LEFT JOIN salesman c ON b.salesman_id = c.salesman_id;
```

**Output:**

<img width="1367" height="666" alt="image" src="https://github.com/user-attachments/assets/f954452b-ff0c-45d3-8f96-48a66872de02" />

**Question 10**
---

Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="1052" height="172" alt="image" src="https://github.com/user-attachments/assets/461ffaa7-77af-4966-8f5c-9854217b1356" />

TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date

<img width="1060" height="171" alt="image" src="https://github.com/user-attachments/assets/c9b14ded-7d5f-49d8-b78c-0e6be2e2da04" />

For example:

<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Patient Name</th>
    <th>Result ID</th>
    <th>Patient ID</th>
    <th>Test Name</th>
    <th>Result</th>
    <th>Test Date</th>
  </tr>
  <tr>
    <td>Alice</td>
    <td>1</td>
    <td>1</td>
    <td>Blood Pressure</td>
    <td>120/80</td>
    <td>2024-01-20</td>
  </tr>
</table>

```sql
SELECT p.first_name AS patient_name, t.* 
FROM patients p 
JOIN test_results t ON p.patient_id = t.patient_id 
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

<img width="1345" height="755" alt="image" src="https://github.com/user-attachments/assets/42507251-c0ea-441d-9a6f-e471200692c5" />

## GRADE :

<img width="1501" height="733" alt="image" src="https://github.com/user-attachments/assets/9e8c3d72-bea1-4db1-8d0b-7985255c1972" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
