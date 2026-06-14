# DBS101 – Database Systems

## Unit IV: Advanced SQL Operations

### Student Information

**Name:** Damchey Lhendup
**Student ID:** 02250347

---

# Unit Overview

This unit builds on the SQL concepts learned previously by introducing advanced SQL operations. It focuses on set operations, handling NULL values, aggregate functions, grouping techniques, subqueries, and data modification commands. These concepts are essential for solving real-world database problems and performing advanced data analysis.

---

# Key Concepts

## Introduction to Advanced SQL

Basic SQL commands are useful for storing and retrieving data, but real-world applications often require more powerful techniques.

Advanced SQL helps users:

* Combine results from multiple queries
* Handle missing information
* Generate reports and summaries
* Perform complex filtering
* Create nested queries

These capabilities make SQL a powerful tool for decision-making and data analysis.

---

# Set Operations

Set operations combine the output of multiple SELECT statements.

---

## Conditions for Set Operations

Before using set operations:

1. Both queries must return the same number of columns.
2. Corresponding columns must have compatible data types.
3. The column names are usually taken from the first query.

---

## Sample Tables

### Student

| StudentID | Name  |
| --------- | ----- |
| 1         | John  |
| 2         | Alice |
| 3         | Bob   |
| 4         | Emma  |

### Teacher

| TeacherID | Name  |
| --------- | ----- |
| 101       | Alice |
| 102       | David |
| 103       | Emma  |

### Alumni

| AlumniID | Name  |
| -------- | ----- |
| 201      | Bob   |
| 202      | Emma  |
| 203      | Henry |

---

## UNION

The UNION operator combines records from two queries and removes duplicates.

### Example

```sql
SELECT Name FROM Student
UNION
SELECT Name FROM Teacher;
```

### Result

| Name  |
| ----- |
| John  |
| Alice |
| Bob   |
| Emma  |
| David |

Duplicate values appear only once.

---

## UNION ALL

UNION ALL combines records but keeps duplicate values.

### Example

```sql
SELECT Name FROM Student
UNION ALL
SELECT Name FROM Teacher;
```

### Result

| Name  |
| ----- |
| John  |
| Alice |
| Bob   |
| Emma  |
| Alice |
| David |
| Emma  |

### Advantage

UNION ALL is faster because duplicate checking is not performed.

---

## INTERSECT

Returns records that exist in both queries.

### Example

```sql
SELECT Name FROM Student
INTERSECT
SELECT Name FROM Alumni;
```

### Result

| Name |
| ---- |
| Bob  |
| Emma |

---

## EXCEPT

Returns records that exist in the first query but not in the second.

### Example

```sql
SELECT Name FROM Student
EXCEPT
SELECT Name FROM Alumni;
```

### Result

| Name  |
| ----- |
| John  |
| Alice |

---

## Summary of Set Operations

| Operation | Purpose                                 |
| --------- | --------------------------------------- |
| UNION     | Combines records and removes duplicates |
| UNION ALL | Combines records and keeps duplicates   |
| INTERSECT | Returns common records                  |
| EXCEPT    | Returns differences                     |

---

# Handling NULL Values

---

## What is NULL?

NULL represents missing, unknown, or unavailable information.

It is not:

* Zero (0)
* Empty string ("")
* Blank space

Instead, it indicates that a value is currently unknown or not provided.

---

## Sample Table

| StudentID | Name  | Age  | Email                                     |
| --------- | ----- | ---- | ----------------------------------------- |
| 1         | John  | 20   | [john@email.com](mailto:john@email.com)   |
| 2         | Alice | NULL | [alice@email.com](mailto:alice@email.com) |
| 3         | Bob   | 19   | NULL                                      |
| 4         | Emma  | 21   | [emma@email.com](mailto:emma@email.com)   |
| 5         | David | NULL | NULL                                      |

---

## Finding NULL Values

```sql
SELECT *
FROM Student
WHERE Age IS NULL;
```

### Result

| StudentID | Name  |
| --------- | ----- |
| 2         | Alice |
| 5         | David |

---

## Finding Non-NULL Values

```sql
SELECT *
FROM Student
WHERE Age IS NOT NULL;
```

---

## Correct Use of NULL

### Incorrect

```sql
WHERE Age = NULL;
```

### Correct

```sql
WHERE Age IS NULL;
```

SQL treats NULL as an unknown value, so it cannot be compared using the equals sign.

---

## Updating NULL Values

```sql
UPDATE Student
SET Age = NULL
WHERE StudentID = 2;
```

---

## Important Note

Aggregate functions such as:

* AVG()
* SUM()
* COUNT(column)

automatically ignore NULL values.

---

# Aggregate Functions

Aggregate functions perform calculations on groups of records and return a single result.

---

## COUNT()

Returns the total number of rows.

```sql
SELECT COUNT(*)
FROM Student;
```

Output:

```text
5
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
| John  | 80    |
| Alice | 90    |
| Bob   | 75    |
| Emma  | 88    |
| David | 70    |

Results:

```text
COUNT = 5
AVG   = 80.6
MAX   = 90
MIN   = 70
```

---

# GROUP BY Clause

The GROUP BY clause groups records that have identical values in a specified column.

### Example

```sql
SELECT Age, COUNT(*)
FROM Student
GROUP BY Age;
```

### Output

| Age  | Count |
| ---- | ----- |
| 20   | 1     |
| 21   | 1     |
| NULL | 2     |
| 19   | 1     |

---

## Applications of GROUP BY

GROUP BY is commonly used for:

* Department statistics
* Student reports
* Sales analysis
* Category summaries

---

# HAVING Clause

The HAVING clause filters grouped data after grouping has taken place.

### Example

```sql
SELECT Age, COUNT(*)
FROM Student
GROUP BY Age
HAVING COUNT(*) > 1;
```

### Result

| Age  | Count |
| ---- | ----- |
| NULL | 2     |

---

## Difference Between WHERE and HAVING

| WHERE                          | HAVING                      |
| ------------------------------ | --------------------------- |
| Filters rows                   | Filters groups              |
| Executed before grouping       | Executed after grouping     |
| Cannot use aggregate functions | Can use aggregate functions |

---

### Example

```sql
SELECT Department, AVG(Marks)
FROM Student
GROUP BY Department
HAVING AVG(Marks) > 70;
```

This displays departments whose average marks exceed 70.

---

# Subqueries

A subquery is a query written inside another SQL query.

The inner query executes first and its result is used by the outer query.

---

## Example 1: Students Above Average Marks

```sql
SELECT Name
FROM Student
WHERE Marks >
(
 SELECT AVG(Marks)
 FROM Student
);
```

### Process

1. Inner query calculates average marks.
2. Outer query finds students above the average.

### Result

| Name  |
| ----- |
| Alice |
| Emma  |

---

## Example 2: Students Enrolled in Courses

### Enrollment Table

| EnrollID | StudentID | Course |
| -------- | --------- | ------ |
| 101      | 1         | DBMS   |
| 102      | 2         | OS     |
| 103      | 4         | Python |

### Query

```sql
SELECT Name
FROM Student
WHERE StudentID IN
(
 SELECT StudentID
 FROM Enrollment
);
```

### Result

| Name  |
| ----- |
| John  |
| Alice |
| Emma  |

---

## Example 3: Highest Marks

```sql
SELECT *
FROM Student
WHERE Marks =
(
 SELECT MAX(Marks)
 FROM Student
);
```

### Result

| Name  | Marks |
| ----- | ----- |
| Alice | 90    |

---

## Advantages of Subqueries

* Simplify complex queries
* Improve readability
* Allow dynamic filtering
* Useful in reporting and analysis

---

# Data Modification Operations

SQL provides commands to insert, update, and delete records.

---

## INSERT Command

Adds new records.

### Example

```sql
INSERT INTO Student
VALUES (6, 'Sonam', 22, 85);
```

---

## UPDATE Command

Modifies existing records.

### Example

```sql
UPDATE Student
SET Marks = 95
WHERE StudentID = 1;
```

---

## DELETE Command

Removes records from a table.

### Example

```sql
DELETE FROM Student
WHERE StudentID = 6;
```

---

## Warning

```sql
DELETE FROM Student;
```

Without a WHERE clause, every record in the table is removed.

---

# Real-World SQL Problem

### Scenario

Retrieve the names and marks of students who:

* Are enrolled in at least one course
* Have no missing information
* Scored above the average marks

### Solution

```sql
SELECT Name, Marks
FROM Student
WHERE StudentID IN
(
 SELECT StudentID
 FROM Enrollment
)
AND Age IS NOT NULL
AND Email IS NOT NULL
AND Marks >
(
 SELECT AVG(Marks)
 FROM Student
);
```

This query combines:

* Subqueries
* Aggregate functions
* NULL handling
* Conditional filtering

to solve a practical database problem.

---

# Quick Revision Notes

* Set Operations:

  * UNION
  * UNION ALL
  * INTERSECT
  * EXCEPT
* NULL Handling:

  * IS NULL
  * IS NOT NULL
* Aggregate Functions:

  * COUNT()
  * SUM()
  * AVG()
  * MAX()
  * MIN()
* GROUP BY groups records.
* HAVING filters grouped results.
* Subqueries are queries inside other queries.
* INSERT, UPDATE, and DELETE modify data.

---

# Unit Summary

This unit introduced advanced SQL features used in real-world database applications. It covered set operations, NULL value handling, aggregate functions, grouping techniques, subqueries, and data modification commands. These concepts allow users to perform complex analysis, generate meaningful reports, and solve practical database problems efficiently.
