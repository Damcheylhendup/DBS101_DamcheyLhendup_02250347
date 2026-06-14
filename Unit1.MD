# DBS101 – Database Systems

## Unit I: Introduction to Database Systems

### Student Information

**Name:** Damchey Lhendup
**Student ID:** 02250347

---

# Unit Overview

This unit introduces the basic concepts of database systems. It explains the meaning of data, information, databases, and database management systems (DBMS). The unit also discusses data abstraction, the evolution of database systems, database users, and database languages.

---

# Key Concepts

## Data

Data refers to raw facts and figures that have not been processed.

### Examples

* Student names
* Employee numbers
* Product prices
* Examination marks

### Sample Data

| Student ID | Name  | Marks |
| ---------- | ----- | ----- |
| 101        | Sonam | 85    |
| 102        | Karma | 90    |
| 103        | Pema  | 78    |

The values stored in the table represent data.

---

## Information

Information is processed data that provides meaning and supports decision-making.

### Example

From the marks table:

* Average Marks = 84.3
* Highest Marks = 90

These results are considered information because they are meaningful outputs derived from data.

---

## Difference Between Data and Information

| Data            | Information     |
| --------------- | --------------- |
| Raw facts       | Processed facts |
| Unorganized     | Organized       |
| Input           | Output          |
| Limited meaning | Meaningful      |

---

# Database

A database is an organized collection of related information stored electronically for easy access and management.

### Examples

* Student Management System
* Banking System
* Hospital Database
* Library Management System

### Features of a Database

* Organized storage
* Shared access
* Reduced redundancy
* Improved consistency
* Easy updates

---

# Database Management System (DBMS)

A DBMS is software that allows users to create, store, manage, and retrieve data from databases.

### Examples of DBMS

**Relational DBMS**

* MySQL
* PostgreSQL
* Oracle Database
* SQL Server

**NoSQL DBMS**

* MongoDB
* Cassandra
* Redis

---

## Main Functions of DBMS

### Data Storage

Stores large amounts of information efficiently.

### Data Retrieval

Provides quick access to required information.

### Data Manipulation

Supports insertion, deletion, and modification of records.

### Security

Protects data from unauthorized access.

### Backup and Recovery

Helps restore data after failures.

### Transaction Management

Maintains consistency during multiple operations.

---

# Advantages of DBMS

* Minimizes duplicate data
* Improves consistency
* Enhances security
* Supports multiple users
* Provides backup facilities
* Maintains data integrity

---

# Disadvantages of DBMS

* Expensive software
* Complex setup
* Requires skilled personnel
* Ongoing maintenance costs

---

# Data Abstraction

Data abstraction hides unnecessary details from users and simplifies database usage.

---

## Physical Level

Describes how data is physically stored.

Examples:

* Disk storage
* File structures
* Indexes

---

## Logical Level

Describes what data is stored and how different data items are related.

Example:

```text
Student
(
 StudentID,
 Name,
 Department
)
```

---

## View Level

Shows only relevant information to specific users.

Example:

**Teacher View**

| StudentID | Name | Marks |

**Administrator View**

| StudentID | Name | Marks | Fees |

---

# Purpose of Database Systems

Database systems were developed to solve the problems found in traditional file-processing systems.

### Problems in File Systems

* Data redundancy
* Data inconsistency
* Difficult access
* Limited sharing
* Security issues

### Objectives of Database Systems

* Reduce redundancy
* Maintain consistency
* Improve sharing
* Enforce integrity
* Enhance security
* Support recovery

---

# Evolution of Database Systems

## File Processing Systems

Used separate files to store information.

### Limitations

* Redundancy
* Inconsistency
* Difficult maintenance

---

## Hierarchical Database Model

Organizes data in a tree structure.

```text
Company
 └── Department
      └── Employee
```

### Advantage

Simple organization.

### Disadvantage

Limited flexibility.

---

## Network Database Model

Allows multiple relationships among records.

```text
Student ↔ Course
```

### Advantage

More flexible.

### Disadvantage

Complex structure.

---

## Relational Database Model

Introduced by Edgar F. Codd.

Uses tables to store information.

### Advantages

* Easy to understand
* Supports SQL
* Flexible structure
* Data independence

---

## Modern Databases

### Object-Oriented Databases

Store data as objects.

### Distributed Databases

Store information across multiple locations.

### Cloud Databases

Hosted on cloud platforms.

### NoSQL Databases

Designed for large-scale applications.

---

# Database Users

## Database Administrator (DBA)

Responsibilities:

* Security management
* Backup and recovery
* Performance monitoring
* User administration

---

## Database Designers

Create database structures and relationships.

---

## Application Programmers

Develop applications that interact with databases.

---

## End Users

Use database applications to perform daily tasks.

Examples:

* Students
* Teachers
* Bank customers

---

# Database Languages

## DDL (Data Definition Language)

Used to define database structures.

Examples:

```sql
CREATE
ALTER
DROP
```

---

## DML (Data Manipulation Language)

Used to manage data.

Examples:

```sql
INSERT
UPDATE
DELETE
```

---

## DQL (Data Query Language)

Used to retrieve information.

Example:

```sql
SELECT
```

---

# Quick Revision Notes

* Data = Raw facts
* Information = Processed data
* Database = Organized collection of data
* DBMS = Software for managing databases
* Three Levels of Abstraction:

  * Physical
  * Logical
  * View
* Main Database Models:

  * Hierarchical
  * Network
  * Relational
* SQL Categories:

  * DDL
  * DML
  * DQL

---

# Unit Summary

This unit provided an introduction to database systems and explained the concepts of data, information, databases, and DBMS. It also covered data abstraction, the purpose of database systems, the evolution of databases, user roles, and database languages. These concepts form the foundation for understanding database design and management.
