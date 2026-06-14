# DBS101 – Database Systems

## Unit V: Relational Database Design and Normalization

### Student Information

**Name:** Damchey Lhendup
**Student ID:** 02250347

---

# Unit Overview

This unit explains the principles of relational database design and normalization. It focuses on reducing data redundancy, preventing anomalies, understanding functional dependencies, and organizing data into well-structured tables. Proper normalization improves consistency, maintenance, and overall database efficiency.

---

# Key Concepts

## Relational Database Design

Relational database design is the process of organizing data into tables so that information can be stored efficiently while avoiding unnecessary duplication.

A properly designed database provides:

* Data consistency
* Data integrity
* Better storage utilization
* Easier maintenance
* Improved query performance

---

## Why Good Database Design Matters

Poor database design often creates problems such as:

* Duplicate data
* Inconsistent records
* Increased storage usage
* Difficult updates
* Maintenance issues

### Example of Poor Design

| StudentID | StudentName | Department | Department Office |
| --------- | ----------- | ---------- | ----------------- |
| 101       | Sonam       | IT         | Block A           |
| 102       | Karma       | IT         | Block A           |
| 103       | Pema        | IT         | Block A           |

The department office information is repeated multiple times, creating redundancy.

---

# Characteristics of a Good Relational Design

A well-designed database should satisfy several important conditions.

---

## 1. Minimal Redundancy

Information should not be stored repeatedly.

For example, department details should be stored separately rather than duplicated for every student record.

---

## 2. No Update Anomaly

An update anomaly occurs when the same information must be changed in multiple locations.

### Example

| StudentID | Department | Office  |
| --------- | ---------- | ------- |
| 101       | IT         | Block A |
| 102       | IT         | Block A |

If the office changes from Block A to Block B, every row must be updated. Missing even one row causes inconsistency.

---

## 3. No Insertion Anomaly

An insertion anomaly occurs when new information cannot be added without entering unrelated data.

Example:

A new department cannot be added unless a student record also exists.

---

## 4. No Deletion Anomaly

A deletion anomaly occurs when deleting one record unintentionally removes other important information.

Example:

Deleting the last student in a department may remove all information about that department.

---

## 5. Dependency Preservation

Functional dependencies should remain enforceable after decomposition.

This ensures data integrity is maintained.

---

## 6. Lossless Join Property

After splitting a table into smaller tables, the original information should be recoverable through join operations.

---

# Functional Dependencies (FD)

---

## Definition

A functional dependency describes a relationship between two attributes.

```text
A → B
```

This means that the value of A uniquely determines the value of B.

---

## Example

| StudentID | StudentName |
| --------- | ----------- |
| 101       | Sonam       |
| 102       | Karma       |

Dependency:

```text
StudentID → StudentName
```

Knowing the StudentID allows us to determine the student's name.

---

# Types of Functional Dependencies

---

## Full Functional Dependency

An attribute depends on the entire primary key.

### Example

```text
Enrollment(StudentID, CourseID, Grade)

(StudentID, CourseID) → Grade
```

The Grade depends on both StudentID and CourseID together.

---

## Partial Dependency

A partial dependency exists when an attribute depends on only part of a composite key.

### Example

```text
(StudentID, CourseID) → StudentName
```

StudentName depends only on StudentID.

This creates redundancy and should be removed.

---

## Transitive Dependency

A transitive dependency occurs when one attribute indirectly determines another.

### Rule

```text
A → B
B → C
Therefore A → C
```

---

### Example

| StudentID | DepartmentID | DepartmentName |
| --------- | ------------ | -------------- |
| 101       | D01          | IT             |

Dependencies:

```text
StudentID → DepartmentID
DepartmentID → DepartmentName
```

Therefore:

```text
StudentID → DepartmentName
```

This is called a transitive dependency.

---

# Decomposition

---

## Definition

Decomposition is the process of dividing a large table into smaller tables to eliminate redundancy and anomalies.

---

## Original Relation

```text
Student
(
 StudentID,
 StudentName,
 DepartmentName,
 DepartmentOffice
)
```

---

## Decomposed Relations

```text
Student
(
 StudentID,
 StudentName,
 DepartmentID
)

Department
(
 DepartmentID,
 DepartmentName,
 DepartmentOffice
)
```

This structure improves organization and reduces duplication.

---

# Properties of Good Decomposition

---

## Lossless Join Decomposition

The original table should be recoverable after decomposition.

Example:

```text
Student JOIN Department
```

The resulting data should match the original relation.

---

## Dependency Preservation

Functional dependencies must remain valid after decomposition.

Example:

```text
DepartmentID → DepartmentName
```

This dependency should still be enforceable.

---

# Normalization

---

## Definition

Normalization is the process of organizing tables to minimize redundancy and remove undesirable dependencies.

The goal is to create efficient and reliable database structures.

---

## Objectives of Normalization

* Remove redundancy
* Improve consistency
* Eliminate anomalies
* Simplify maintenance
* Enhance data integrity

---

## Hierarchy of Normal Forms

```text
1NF → 2NF → 3NF → BCNF → 4NF
```

Each level removes additional database design problems.

---

# First Normal Form (1NF)

A table is in First Normal Form when:

* Every attribute contains atomic values.
* No repeating groups exist.

---

## Example Not in 1NF

| StudentID | Name  | PhoneNumbers       |
| --------- | ----- | ------------------ |
| 101       | Sonam | 17111111, 17222222 |

Multiple values exist in a single column.

---

## Converted to 1NF

| StudentID | Name  | PhoneNumber |
| --------- | ----- | ----------- |
| 101       | Sonam | 17111111    |
| 101       | Sonam | 17222222    |

Each field now contains only one value.

---

# Second Normal Form (2NF)

A table is in Second Normal Form if:

1. It is already in 1NF.
2. It contains no partial dependencies.

---

## Example with Partial Dependency

```text
Enrollment
(
 StudentID,
 CourseID,
 StudentName
)

Primary Key:
(StudentID, CourseID)
```

Dependency:

```text
StudentID → StudentName
```

StudentName depends only on StudentID.

---

## Converted to 2NF

```text
Student
(
 StudentID,
 StudentName
)

Enrollment
(
 StudentID,
 CourseID
)
```

The partial dependency is removed.

---

# Third Normal Form (3NF)

A relation is in Third Normal Form if:

1. It is already in 2NF.
2. It contains no transitive dependencies.

---

## Example

| StudentID | DepartmentID | DepartmentName |
| --------- | ------------ | -------------- |

Dependencies:

```text
StudentID → DepartmentID
DepartmentID → DepartmentName
```

DepartmentName depends indirectly on StudentID.

---

## Converted to 3NF

```text
Student
(
 StudentID,
 DepartmentID
)

Department
(
 DepartmentID,
 DepartmentName
)
```

---

## Benefits of 3NF

* Less redundancy
* Better consistency
* Easier maintenance
* Improved data integrity

---

# Boyce-Codd Normal Form (BCNF)

BCNF is a stronger version of Third Normal Form.

A table is in BCNF when every determinant is a candidate key.

Rule:

```text
X → Y
```

X must always be a candidate key.

---

## Example

```text
Course
(
 Teacher,
 Subject,
 Room
)

Teacher → Subject
Subject → Room
```

Although this may satisfy 3NF, it can still violate BCNF.

Further decomposition may be necessary.

---

# Fourth Normal Form (4NF)

A table is in Fourth Normal Form when:

1. It satisfies BCNF.
2. It contains no multivalued dependencies.

---

## Example

| Student | Hobby    | Language |
| ------- | -------- | -------- |
| Sonam   | Football | English  |
| Sonam   | Football | Dzongkha |
| Sonam   | Music    | English  |
| Sonam   | Music    | Dzongkha |

The combinations create unnecessary redundancy.

---

## Converted to 4NF

```text
StudentHobby
(
 Student,
 Hobby
)

StudentLanguage
(
 Student,
 Language
)
```

The multivalued dependency is removed.

---

# Comparison of Normal Forms

| Normal Form | Problem Removed                           |
| ----------- | ----------------------------------------- |
| 1NF         | Repeating groups                          |
| 2NF         | Partial dependencies                      |
| 3NF         | Transitive dependencies                   |
| BCNF        | Remaining functional dependency anomalies |
| 4NF         | Multivalued dependencies                  |

---

# Practical Example of Normalization

## Original Relation

| StudentID | StudentName | DeptID | DeptName |
| --------- | ----------- | ------ | -------- |

Problems:

* Repeated department names
* Update anomalies
* Deletion anomalies
* Redundant data

---

## Normalized Relations

```text
Student
(
 StudentID,
 StudentName,
 DeptID
)

Department
(
 DeptID,
 DeptName
)
```

---

## Benefits

* Reduced redundancy
* Improved consistency
* Easier updates
* Better maintenance
* Higher data integrity

---

# Quick Revision Notes

* Good design minimizes redundancy.
* Functional Dependency:

  * Full Dependency
  * Partial Dependency
  * Transitive Dependency
* Decomposition should be:

  * Lossless
  * Dependency Preserving
* Normal Forms:

  * 1NF → Atomic values
  * 2NF → No partial dependency
  * 3NF → No transitive dependency
  * BCNF → Every determinant is a candidate key
  * 4NF → No multivalued dependency
* Normalization reduces anomalies.

---

# Unit Summary

This unit explained the principles of relational database design and the importance of reducing redundancy. It introduced functional dependencies, decomposition techniques, and normalization. The concepts of 1NF, 2NF, 3NF, BCNF, and 4NF were explored to demonstrate how databases can be organized into efficient, consistent, and anomaly-free structures. Proper normalization helps improve database performance, maintainability, and data integrity.
