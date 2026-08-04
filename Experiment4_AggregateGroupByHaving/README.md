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
-- Paste Question 6 here

```sql
-- Paste your SQL code below for Question 6
```

**Output:**

![Output6](output.png)

**Question 7**
---
-- Paste Question 7 here

```sql
-- Paste your SQL code below for Question 7
```

**Output:**

![Output7](output.png)

**Question 8**
---
-- Paste Question 8 here

```sql
-- Paste your SQL code below for Question 8
```

**Output:**

![Output8](output.png)

**Question 9**
---
-- Paste Question 9 here

```sql
-- Paste your SQL code below for Question 9
```

**Output:**

![Output9](output.png)

**Question 10**
---
-- Paste Question 10 here

```sql
-- Paste your SQL code below for Question 10
```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
