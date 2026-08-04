## Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many patients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?

Sample table: Patients Table

<img width="1076" height="161" alt="image" src="https://github.com/user-attachments/assets/649bef99-56e2-4f85-8fb5-dcef326fe4ca" />

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>AgeGroup    TotalPatients
----------  -------------
20-30       1
31-40       5
41-50       3
Above 50    1</pre></td>
  </tr>
</table>


```sql
SELECT CASE 
WHEN (2024-STRFTIME('%Y',DateOfBirth))<20 THEN 'Under 20' 
WHEN (2024-STRFTIME('%Y',DateOfBirth)) BETWEEN 20 AND 30 THEN '20-30' 
WHEN (2024-STRFTIME('%Y',DateOfBirth)) BETWEEN 31 AND 40 THEN '31-40'
WHEN (2024-STRFTIME('%Y',DateOfBirth)) BETWEEN 41 AND 50 THEN '41-50'
ELSE 'Above 50'
END AS AgeGroup,
COUNT(*) AS TotalPatients
FROM Patients
GROUP BY AgeGroup

```

**Output:**

<img width="1310" height="808" alt="image" src="https://github.com/user-attachments/assets/a581d9b0-0a86-4803-b2dc-232f900c4d54" />

**Question 2**
---
How many medical records were created in each month?

Sample table:MedicalRecords Table

<img width="1089" height="164" alt="image" src="https://github.com/user-attachments/assets/cb2327a8-4182-465a-9f8e-88387fb776d8" />

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>Month       TotalRecords
----------  ------------
2023-12     2
2024-01     6
2024-02     2</pre></td>
  </tr>
</table>


```sql
SELECT SUBSTR(Date,1,7) AS Month,
COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY Month;
```

**Output:**

<img width="1289" height="804" alt="Screenshot 2026-08-04 143333" src="https://github.com/user-attachments/assets/feeca6ca-8d6e-4bdf-b86e-8fdcda82f137" />

**Question 3**
---
Write SQL query to extract the email domain from each patient's email address and count the number of patients with the same email domain.

Sample table: Patients Table

<img width="1076" height="161" alt="image" src="https://github.com/user-attachments/assets/d84e6843-1de9-4279-84c9-df39a6264bd5" />

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>EmailDomain  TotalPatients
-----------  -------------
example.com  10</pre></td>
  </tr>
</table>


```sql
SELECT SUBSTR(EMail,INSTR(Email,'@')+1) AS EmailDomain,
COUNT(*) AS TotalPatients
FROM Patients
GROUP BY EmailDomain;
```

**Output:**

<img width="1284" height="756" alt="image" src="https://github.com/user-attachments/assets/c1e6f304-6145-48eb-80dc-fd51fa2d3872" />

**Question 4**
---
Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 

Note: Inventory attribute contains amount of fruits

Table: fruits
```
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
```

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>total_available_amount
----------------------
160</pre></td>
  </tr>
</table>

```sql
SELECT SUM(inventory) AS total_available_amount
FROM fruits
WHERE price>0.5;
```

**Output:**

<img width="1261" height="797" alt="image" src="https://github.com/user-attachments/assets/4a868d91-ae2c-425e-922c-c35f8e98d073" />

**Question 5**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

| id | name | age | address | salary |
|----|------|-----|-----------|--------|
| 1 | Paul | 32 | California | 20000 |
| 4 | Mark | 25 | Richtown | 65000 |
| 5 | David | 27 | Texas | 85000 |

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>COUNT
----------
5</pre></td>
  </tr>
</table>

```sql
SELECT COUNT(*) AS COUNT
FROM employee
WHERE age>32;
```

**Output:**

<img width="1263" height="800" alt="image" src="https://github.com/user-attachments/assets/f4b9d86f-961f-411a-af20-f9fb89d53ea6" />

**Question 6**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits
```
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
```

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>fruit_name  lowest_quantity
----------  ---------------
Watermelon  15</pre></td>
  </tr>
</table>


```sql
SELECT name AS fruit_name, inventory AS lowest_quantity
FROM fruits
WHERE inventory = ( SELECT MIN(inventory) FROM fruits);
```

**Output:**

<img width="1265" height="791" alt="Screenshot 2026-08-04 144041" src="https://github.com/user-attachments/assets/aa6bb4ce-1505-4ac8-b307-dcd674a81695" />

**Question 7**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders
```
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>MINIMUM
----------
65.26</pre></td>
  </tr>
</table>

```sql
SELECT MIN(purch_amt) AS MINIMUM FROM orders;
```

**Output:**

<img width="1269" height="793" alt="Screenshot 2026-08-04 144156" src="https://github.com/user-attachments/assets/c55fd973-ee35-4182-9de2-b904b592b3e5" />

**Question 8**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1

<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/b4e5bfc1-c95e-4348-b522-19944b320ccd" />

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>age_group   AVG(age)
----------  ----------
20          23.0</pre></td>
  </tr>
</table>

```sql
SELECT (age/5) * 5 AS age_group, AVG(age)
FROM customer1
GROUP BY age_group
HAVING AVG(age)<24;
```

**Output:**

<img width="1263" height="790" alt="Screenshot 2026-08-04 144342" src="https://github.com/user-attachments/assets/fcce8730-c8e0-4667-9154-fdaf9a24e0de" />

**Question 9**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1

<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/72b6d5e7-4e8e-4527-a5f4-e0c9287377a6" />

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>age_group   MAX(salary)
----------  -----------
20          10000
25          8500</pre></td>
  </tr>
</table>

```sql
SELECT (age/5)*5 AS age_group, 
MAX(salary) AS "MAX(salary)"
FROM customer1
GROUP BY age_group
HAVING MAX(salary)>8000;
```

**Output:**

<img width="1296" height="762" alt="Screenshot 2026-08-04 144513" src="https://github.com/user-attachments/assets/a6e14641-5e71-4b24-a5ef-e7b473a2e5c4" />

**Question 10**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

<img width="972" height="212" alt="image" src="https://github.com/user-attachments/assets/0a7a1a8e-e6cb-47c1-90d4-c4d738e7b186" />

For example:

<table>
  <tr>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>category_id  count(product_name)
-----------  -------------------
1            4
2            3</pre></td>
  </tr>
</table>

```sql
SELECT category_id,count(product_name)
FROM products 
GROUP BY category_id
HAVING MIN(category_id)<3;
```

**Output:**

<img width="1295" height="773" alt="Screenshot 2026-08-04 144626" src="https://github.com/user-attachments/assets/abfd8c3c-30eb-4b30-a789-846e9a38fe57" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
