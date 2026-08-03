# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

For example:
<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>SELECT * FROM Employee WHERE EmployeeID = 001;</pre></td>
    <td><pre>EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
1           Sarah Parker  Manager     HR          60000</pre></td>
  </tr>
</table>

```sql
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary)
VALUES ('1','Sarah Parker','Manager','HR',60000);
```

**Output:**

<img width="1219" height="806" alt="image" src="https://github.com/user-attachments/assets/5ade562d-1cd0-4ec1-8f07-5d93a69bf6f5" />

**Question 2**
---
Create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

For example:
<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>INSERT INTO jobs (job_id, job_title, min_salary, max_salary)
VALUES (1, 'Software Engineer', 9000, 15000);

SELECT * FROM jobs;</pre></td> <td><pre>job_id      job_title          min_salary  max_salary

---

1           Software Engineer  9000        15000</pre></td>

  </tr>
</table>


```sql
CREATE TABLE jobs(job_id INT,job_title VARCHAR(100) DEFAULT '',min_salary DECIMAL(10,2) DEFAULT 8000.00,max_salary DECIMAL(10,2) DEFAULT NULL);
```

**Output:**

<img width="1278" height="784" alt="image" src="https://github.com/user-attachments/assets/6b91e5dc-9bb3-4414-b3a4-c4c86790f590" />

**Question 3**
---
Write a SQL query to Add a new column Country as text in the Student_details table.

**Sample table: Student_details**

```text
cid  name     type         notnull  dflt_value  pk
---  -------  -----------  -------  ----------  --
0    RollNo   int          0                    1
1    Name     VARCHAR(10)  1                    0
2    Gender   TEXT         1                    0
3    Subject  VARCHAR(30)  0                    0
4    MARKS    INT(3)       0                    0
5    Country  TEXT         0                    0
```

For example:

<table>
  <tr>
    <th>Test</th>
    <th>Result</th>
  </tr>
  <tr>
    <td><pre>PRAGMA table_info('Student_details');</pre></td>
    <td><pre>cid  name     type         notnull  dflt_value  pk
---  -------  -----------  -------  ----------  --
0    RollNo   INT          0                    1
1    Name     VARCHAR(10)  1                    0
2    Gender   TEXT         1                    0
3    Subject  VARCHAR(30)  0                    0
4    MARKS    INT(3)       0                    0
5    Country  TEXT         0                    0</pre></td>
  </tr>
</table>

```sql
ALTER TABLE Student_details
ADD COLUMN Country TEXT;
```

**Output:**

<img width="1283" height="814" alt="image" src="https://github.com/user-attachments/assets/85a628b4-b50f-4703-85b1-ed3544231f9c" />

**Question 4**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

For example:


```sql
-- Paste your SQL code below for Question 4
```

**Output:**

![Output4](output.png)

**Question 5**
---
-- Paste Question 5 here

```sql
-- Paste your SQL code below for Question 5
```

**Output:**

![Output5](output.png)

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
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
