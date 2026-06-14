# DBS101 – Database Systems

## Unit III: Introduction to SQL (Structured Query Language)

### Student Information

**Name:** Damchey Lhendup
**Student ID:** 02250347

---

# Unit Overview

This unit introduces SQL (Structured Query Language), the standard language used to interact with relational databases. It covers different categories of SQL commands, table creation and modification, data retrieval, constraints, filtering techniques, aggregate functions, and grouping operations.

---

# Key Concepts

## What is SQL?

SQL stands for Structured Query Language. It is the standard language used to create, manage, and manipulate relational databases.

Using SQL, users can:

* Create databases
* Create tables
* Insert records
* Retrieve information
* Update data
* Delete records

Popular database systems that use SQL include:

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server

---

## Why SQL is Important

SQL is widely used because it provides an efficient way to work with large amounts of data.

### Advantages of SQL

* Easy to learn
* Powerful query language
* Handles large databases efficiently
* Standard across different DBMS platforms
* Supports fast data retrieval

---

## Example Student Table

| StudentID | Name  | Age |
| --------- | ----- | --- |
| 101       | Sonam | 20  |
| 102       | Karma | 21  |
| 103       | Pema  | 19  |

Example query:

```sql
SELECT * FROM Student;
```

This statement retrieves all records from the Student table.

---

# Categories of SQL Commands

SQL commands are divided into different categories based on their purpose.

```text
SQL
├── DDL
├── DML
├── DQL
├── DCL
└── TCL
```

---

## DDL (Data Definition Language)

DDL commands are used to define and modify database structures.

### Common DDL Commands

* CREATE
* ALTER
* DROP
* TRUNCATE

---

# CREATE Command

Used to create new database objects such as tables.

### Example

```sql
CREATE TABLE Student
(
 StudentID INT,
 Name VARCHAR(50),
 Age INT
);
```

This creates a Student table with three columns.

---

# ALTER Command

Used to modify an existing table.

### Adding a Column

```sql
ALTER TABLE Student
ADD Email VARCHAR(100);
```

### Modifying a Column

```sql
ALTER TABLE Student
MODIFY Name VARCHAR(100);
```

---

# DROP Command

Removes a table completely from the database.

### Example

```sql
DROP TABLE Student;
```

### Important Note

When a table is dropped:

* Table structure is removed
* All records are deleted permanently

---

# TRUNCATE Command

Removes all records while keeping the table structure.

### Example

```sql
TRUNCATE TABLE Student;
```

---

## DROP vs TRUNCATE

| DROP                    | TRUNCATE                |
| ----------------------- | ----------------------- |
| Deletes table structure | Keeps table structure   |
| Removes all records     | Removes all records     |
| Table no longer exists  | Table remains available |

---

# SQL Constraints

Constraints are rules that ensure data accuracy and integrity.

---

## PRIMARY KEY

A primary key uniquely identifies every record in a table.

### Characteristics

* Unique
* Cannot contain NULL values

### Example

```sql
CREATE TABLE Student
(
 StudentID INT PRIMARY KEY,
 Name VARCHAR(50)
);
```

---

## FOREIGN KEY

A foreign key creates a relationship between two tables.

### Example

```sql
CREATE TABLE Course
(
 CourseID INT PRIMARY KEY,
 StudentID INT,
 FOREIGN KEY(StudentID)
 REFERENCES Student(StudentID)
);
```

---

## UNIQUE Constraint

Prevents duplicate values.

### Example

```sql
Email VARCHAR(100) UNIQUE
```

---

## NOT NULL Constraint

Ensures a column always contains a value.

### Example

```sql
Name VARCHAR(50) NOT NULL
```

---

## CHECK Constraint

Restricts values according to a condition.

### Example

```sql
Age INT CHECK(Age >= 18)
```

Only ages greater than or equal to 18 are allowed.

---

## DEFAULT Constraint

Assigns a default value automatically.

### Example

```sql
Country VARCHAR(20) DEFAULT 'Bhutan'
```

If no value is entered, Bhutan will be stored automatically.

---

# DML (Data Manipulation Language)

DML commands are used to insert, update, and delete records.

---

## INSERT Command

Adds new records to a table.

### Example

```sql
INSERT INTO Student
VALUES (101, 'Sonam', 20);
```

### Multiple Record Insertion

```sql
INSERT INTO Student
VALUES
(102, 'Karma', 21),
(103, 'Pema', 19);
```

---

## UPDATE Command

Used to modify existing records.

### Example

```sql
UPDATE Student
SET Age = 22
WHERE StudentID = 101;
```

This changes the age of StudentID 101.

---

## DELETE Command

Removes records from a table.

### Example

```sql
DELETE FROM Student
WHERE StudentID = 101;
```

### Warning

```sql
DELETE FROM Student;
```

Without a WHERE clause, every record in the table will be deleted.

---

# DQL (Data Query Language)

DQL is used to retrieve information from databases.

The most commonly used command is:

```sql
SELECT
```

---

## Retrieving All Columns

```sql
SELECT *
FROM Student;
```

Returns every column and row.

---

## Retrieving Specific Columns

```sql
SELECT Name, Age
FROM Student;
```

Returns only the Name and Age columns.

---

# WHERE Clause

The WHERE clause filters records based on conditions.

### Example

```sql
SELECT *
FROM Student
WHERE Age > 20;
```

Only students older than 20 will be displayed.

---

## Comparison Operators

| Operator | Meaning                  |
| -------- | ------------------------ |
| =        | Equal To                 |
| >        | Greater Than             |
| <        | Less Than                |
| >=       | Greater Than or Equal To |
| <=       | Less Than or Equal To    |
| <>       | Not Equal To             |

---

# Logical Operators

Logical operators combine multiple conditions.

---

## AND Operator

All conditions must be true.

```sql
SELECT *
FROM Student
WHERE Age > 18
AND Age < 25;
```

---

## OR Operator

At least one condition must be true.

```sql
SELECT *
FROM Student
WHERE Name = 'Sonam'
OR Name = 'Karma';
```

---

## NOT Operator

Returns records that do not satisfy a condition.

```sql
SELECT *
FROM Student
WHERE NOT Age = 20;
```

---

# ORDER BY Clause

Used to sort query results.

### Ascending Order

```sql
SELECT *
FROM Student
ORDER BY Age ASC;
```

### Descending Order

```sql
SELECT *
FROM Student
ORDER BY Age DESC;
```

---

# DISTINCT Keyword

Used to eliminate duplicate values.

### Example

```sql
SELECT DISTINCT Department
FROM Student;
```

Only unique department names are displayed.

---

# Additional SQL Operations

---

## LIKE Operator

Used for pattern matching.

### Names Starting with S

```sql
SELECT *
FROM Student
WHERE Name LIKE 'S%';
```

### Names Ending with m

```sql
SELECT *
FROM Student
WHERE Name LIKE '%m';
```

### Names Containing a

```sql
SELECT *
FROM Student
WHERE Name LIKE '%a%';
```

---

## BETWEEN Operator

Selects values within a specified range.

### Example

```sql
SELECT *
FROM Student
WHERE Age BETWEEN 18 AND 25;
```

---

## IN Operator

Checks whether a value exists in a list.

### Example

```sql
SELECT *
FROM Student
WHERE Department IN ('IT', 'CS');
```

---

## Alias (AS)

Provides a temporary name for a column.

### Example

```sql
SELECT Name AS StudentName
FROM Student;
```

---

# Aggregate Functions

Aggregate functions perform calculations on groups of records.

---

## COUNT()

Counts the number of rows.

```sql
SELECT COUNT(*)
FROM Student;
```

---

## SUM()

Calculates the total value.

```sql
SELECT SUM(Marks)
FROM Student;
```

---

## AVG()

Calculates the average value.

```sql
SELECT AVG(Marks)
FROM Student;
```

---

## MAX()

Returns the highest value.

```sql
SELECT MAX(Marks)
FROM Student;
```

---

## MIN()

Returns the lowest value.

```sql
SELECT MIN(Marks)
FROM Student;
```

---

## Example

| Name  | Marks |
| ----- | ----- |
| Sonam | 80    |
| Karma | 90    |
| Pema  | 70    |

Query:

```sql
SELECT AVG(Marks)
FROM Student;
```

Result:

```text
80
```

---

# GROUP BY Clause

The GROUP BY clause groups records that have the same values.

### Example

```sql
SELECT Department, COUNT(*)
FROM Student
GROUP BY Department;
```

### Sample Output

| Department | Count |
| ---------- | ----- |
| IT         | 5     |
| CS         | 3     |

---

# HAVING Clause

The HAVING clause filters grouped data after grouping.

### Example

```sql
SELECT Department, COUNT(*)
FROM Student
GROUP BY Department
HAVING COUNT(*) > 2;
```

Only departments with more than two records will be displayed.

---

## WHERE vs HAVING

| WHERE                    | HAVING                  |
| ------------------------ | ----------------------- |
| Filters rows             | Filters groups          |
| Executed before grouping | Executed after grouping |

---

# Example of a Complete Query

```sql
SELECT Department, AVG(Marks)
FROM Student
WHERE Age > 18
GROUP BY Department
HAVING AVG(Marks) > 70
ORDER BY AVG(Marks) DESC;
```

This query:

1. Selects students older than 18.
2. Groups them by department.
3. Calculates average marks.
4. Filters departments with averages above 70.
5. Sorts results in descending order.

---

# SQL Query Execution Order

SQL processes statements in the following order:

```text
FROM
 ↓
WHERE
 ↓
GROUP BY
 ↓
HAVING
 ↓
SELECT
 ↓
ORDER BY
```

Understanding this sequence helps write more efficient queries.

---

# Quick Revision Notes

* SQL = Structured Query Language
* Main Categories:

  * DDL
  * DML
  * DQL
  * DCL
  * TCL
* Common DDL Commands:

  * CREATE
  * ALTER
  * DROP
  * TRUNCATE
* Common DML Commands:

  * INSERT
  * UPDATE
  * DELETE
* Important Constraints:

  * PRIMARY KEY
  * FOREIGN KEY
  * UNIQUE
  * NOT NULL
  * CHECK
  * DEFAULT
* Aggregate Functions:

  * COUNT()
  * SUM()
  * AVG()
  * MAX()
  * MIN()

---

# Unit Summary

This unit introduced SQL and its role in managing relational databases. It covered the major categories of SQL commands, table creation and modification, data manipulation, constraints, filtering techniques, aggregate functions, and grouping operations. Understanding SQL is essential because it serves as the primary language for interacting with database systems and retrieving meaningful information from stored data.
