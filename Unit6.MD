# DBS101 – Database Systems

## Unit VI: Indexing and Query Processing

### Student Information

**Name:** Damchey Lhendup
**Student ID:** 02250347

---

# Unit Overview

This unit introduces indexing and query processing in database systems. It explains how indexes improve data retrieval speed, describes different indexing structures, compares B-Tree and B+ Tree indexing, and discusses query processing and optimization techniques used to improve database performance.

---

# Key Concepts

## Introduction to Indexing

### What is Indexing?

Indexing is a technique used to speed up data retrieval by creating a separate structure that stores search keys and references to actual records.

An index works much like the index found at the back of a textbook. Instead of searching through every page, users can quickly locate the required information.

---

## Why Indexing is Important

Without indexing, the database must search through records one by one.

With indexing, records can be found much faster because the search is directed to the correct location.

---

## Benefits of Indexing

* Faster data retrieval
* Reduced disk access
* Improved query performance
* Better response time
* Efficient searching in large databases

---

## Example Without an Index

### Student Table

| ID | Name  | Age |
| -- | ----- | --- |
| 1  | Sonam | 20  |
| 2  | Karma | 21  |
| 3  | Pema  | 19  |
| 4  | Tashi | 22  |

Query:

```sql
SELECT * FROM Student
WHERE Name = 'Pema';
```

Search Process:

```text
Sonam → Karma → Pema
```

The database checks multiple records before finding the required one.

---

## Example With an Index

### Index Table

| Name  | Pointer |
| ----- | ------- |
| Karma | Row 2   |
| Pema  | Row 3   |
| Sonam | Row 1   |
| Tashi | Row 4   |

Search Process:

```text
Pema → Row 3
```

The required record is found directly.

---

## Components of an Index

Every index consists of:

1. Search Key
2. Pointer to Data Record

These components help locate records quickly.

---

# Indexing Structures

Databases use different indexing methods depending on data size and performance requirements.

---

## Single-Level Index

A single-level index contains key values and pointers to data blocks.

### Example

```text
10 → Block1
20 → Block2
30 → Block3
40 → Block4
```

---

### Advantages

* Easy to implement
* Faster than linear searching

### Disadvantages

* Less effective for large databases
* Performance decreases as data grows

---

## Multi-Level Index

A multi-level index creates additional indexes on top of existing indexes.

### Structure

```text
Level 2 Index
      ↓
Level 1 Index
      ↓
Data File
```

This significantly reduces the search area.

---

### Advantages

* Faster searching
* Suitable for large databases
* Better scalability

### Disadvantages

* Requires additional storage
* More difficult to maintain

---

# Tree-Based Indexing

Most modern DBMS use tree-based indexing because it provides efficient searching and updating.

The two most common structures are:

* B-Tree
* B+ Tree

---

# B-Tree

A B-Tree is a self-balancing tree structure used to organize index entries efficiently.

---

## Example

```text
         50
       /    \
     20      80
    /  \    /  \
  10  30  70  90
```

---

## Characteristics of B-Tree

### Balanced Structure

All leaf nodes remain at approximately the same level.

### Sorted Data

Keys are stored in sorted order.

### Multiple Child Nodes

Each node may contain multiple children.

### Dynamic Updates

Insertion, deletion, and updates can be performed efficiently.

---

## Search Complexity

The search time in a B-Tree is:

```text
O(log n)
```

This is significantly faster than linear searching.

---

## Conditions of a B-Tree

1. All leaf nodes are at the same level.
2. Keys remain sorted.
3. Empty subtrees are not allowed.
4. Tree height remains minimal.

---

# B+ Tree

The B+ Tree is an improved version of the B-Tree and is the indexing structure most commonly used in modern database systems.

Examples include:

* MySQL
* PostgreSQL
* Oracle Database

---

## Structure of a B+ Tree

```text
          [30]
         /    \
      [10]   [50]
       / \    / \
     L1 L2  L3 L4
```

---

## Important Characteristics

### Internal Nodes

Store only search keys.

### Leaf Nodes

Store search keys along with pointers to records.

### Linked Leaf Nodes

Leaf nodes are connected sequentially.

```text
L1 ↔ L2 ↔ L3 ↔ L4
```

This allows efficient sequential access.

---

## Advantages of B+ Tree

### Faster Searching

Every search follows a predictable path.

---

### Efficient Range Queries

Example:

```sql
SELECT *
FROM Student
WHERE Marks BETWEEN 60 AND 80;
```

Because leaf nodes are linked, range searches are very efficient.

---

### Better Sequential Access

Records can be accessed in order without repeatedly traversing the tree.

---

### Improved Storage Utilization

Internal nodes contain only keys, allowing more efficient use of space.

---

# B-Tree vs B+ Tree

| B-Tree                                 | B+ Tree                           |
| -------------------------------------- | --------------------------------- |
| Data stored in internal and leaf nodes | Data stored only in leaf nodes    |
| Less efficient for range searches      | More efficient for range searches |
| Less commonly used                     | Widely used in modern DBMS        |

---

# Query Processing

## Definition

Query processing refers to the activities performed by a DBMS to convert a SQL query into an efficient execution plan and return the required results.

---

## Stages of Query Processing

```text
SQL Query
    ↓
Parsing
    ↓
Validation
    ↓
Optimization
    ↓
Execution
    ↓
Result
```

---

## Stage 1: Parsing

The DBMS checks whether the SQL statement follows correct syntax rules.

### Correct Query

```sql
SELECT *
FROM Student;
```

### Incorrect Query

```sql
SELEC *
FROM Student;
```

The second statement contains a syntax error.

---

## Stage 2: Validation

The DBMS verifies:

* Table names
* Column names
* User permissions
* Database objects

Only valid queries proceed further.

---

## Stage 3: Query Optimization

The DBMS determines the most efficient way to execute the query.

Possible strategies include:

* Full table scan
* Index scan
* Join optimization

---

## Stage 4: Query Execution

The selected execution plan is carried out and results are returned to the user.

---

## Example of Query Processing

```sql
SELECT Name
FROM Student
WHERE StudentID = 101;
```

Processing Flow:

```text
Parse Query
      ↓
Validate Query
      ↓
Use Primary Key Index
      ↓
Retrieve Record
      ↓
Return Result
```

---

# Query Optimization

## Definition

Query optimization is the process of selecting the most efficient execution plan for a query.

The objective is to reduce processing cost and improve performance.

Without optimization, queries on large databases may consume excessive CPU, memory, and disk resources.

---

# Query Optimization Techniques

---

## 1. Use Indexes

Indexes allow direct access to records.

### Example

```sql
SELECT *
FROM Student
WHERE StudentID = 1001;
```

An index enables faster retrieval.

---

## 2. Avoid SELECT *

Retrieving unnecessary columns increases overhead.

### Less Efficient

```sql
SELECT *
FROM Student;
```

### Better Approach

```sql
SELECT Name
FROM Student;
```

Only required columns are retrieved.

---

## 3. Use Effective WHERE Conditions

Filtering records reduces the search space.

### Example

```sql
SELECT *
FROM Student
WHERE Department = 'IT';
```

This allows the DBMS to process fewer rows.

---

## 4. Use Efficient Joins

Joining indexed columns improves performance.

### Example

```sql
SELECT *
FROM Student S
JOIN Department D
ON S.DepartmentID = D.DepartmentID;
```

---

## 5. Avoid Unnecessary Calculations

Repeated calculations increase processing time.

Queries should be written efficiently to reduce workload.

---

# Query Cost

The optimizer estimates:

* CPU usage
* Memory usage
* Disk I/O operations

The plan with the lowest estimated cost is chosen.

---

# Role of Indexing in Query Optimization

Indexing is one of the most important factors affecting query performance.

---

## Faster Searching

### Without Index

```text
O(n)
```

Records are searched sequentially.

### With Index

```text
O(log n)
```

Records can be located much faster.

---

## Reduced Disk Access

Indexes decrease the number of disk reads required to locate information.

---

## Improved Join Performance

Indexed columns help databases perform joins more efficiently.

---

## Faster Sorting

Indexes can assist ORDER BY operations and reduce sorting overhead.

---

## Practical Example

### Without Index

```sql
SELECT *
FROM Student
WHERE Name = 'Sonam';
```

Search Process:

```text
Row1 → Row2 → Row3 → ... → Row100000
```

Many records may need to be checked.

---

### With Index

```text
Index
 ↓
Sonam
 ↓
Row 450
```

The desired record is located directly.

---

# Quick Revision Notes

* Indexing improves data retrieval speed.
* Main Index Components:

  * Search Key
  * Record Pointer
* Index Types:

  * Single-Level Index
  * Multi-Level Index
* Tree-Based Indexes:

  * B-Tree
  * B+ Tree
* Query Processing Stages:

  * Parsing
  * Validation
  * Optimization
  * Execution
* Query Optimization Techniques:

  * Use indexes
  * Avoid SELECT *
  * Use proper WHERE clauses
  * Optimize joins
  * Reduce unnecessary calculations
* Search Complexity:

  * Without Index = O(n)
  * With Index = O(log n)

---

# Unit Summary

This unit introduced indexing and query processing techniques used in modern database systems. It explained how indexes improve search efficiency, discussed single-level and multi-level indexing structures, and compared B-Tree and B+ Tree indexes. The unit also covered the stages of query processing and various optimization techniques that improve performance. Understanding these concepts helps database designers create faster and more efficient database systems.
