# DBS101 – Database Systems

## Unit II: Database Design and Entity–Relationship (ER) Model

### Student Information

**Name:** Damchey Lhendup
**Student ID:** 02250347

---

# Unit Overview

This unit focuses on database design and the Entity–Relationship (ER) Model. It explains how databases are planned and structured, introduces entities, attributes, relationships, keys, and ER diagrams, and demonstrates how conceptual database models are converted into relational schemas.

---

# Key Concepts

## Database Design

Database design is the process of organizing and structuring a database so that data can be stored, maintained, and retrieved efficiently.

A well-designed database helps reduce redundancy, improve consistency, and ensure data integrity.

### Objectives of Database Design

* Reduce duplicate data
* Maintain consistency
* Improve integrity
* Support efficient queries
* Simplify maintenance
* Enhance security

---

# Importance of Database Design

Poor database design can cause several problems:

* Duplicate information
* Inconsistent records
* Difficult maintenance
* Slow query execution
* Wasted storage space

### Example of Poor Design

| StudentID | StudentName | Department | Office  |
| --------- | ----------- | ---------- | ------- |
| 101       | Sonam       | IT         | Block A |
| 102       | Karma       | IT         | Block A |

The office information is stored repeatedly.

### Improved Design

#### Student Table

| StudentID | StudentName | DepartmentID |

#### Department Table

| DepartmentID | DepartmentName | Office |

This design removes redundancy and improves efficiency.

---

# Database Design Process

Database development generally follows four stages.

```text
Requirements Collection
         ↓
Conceptual Design
         ↓
Logical Design
         ↓
Physical Design
```

---

## 1. Requirements Collection and Analysis

The first stage focuses on understanding organizational needs.

### Activities

* Gather data requirements
* Understand business rules
* Consult stakeholders
* Identify relationships

### Example

For a university database, information may be required about:

* Students
* Courses
* Instructors
* Enrollments

Questions include:

* What student information should be stored?
* Can students enroll in multiple courses?
* Who will access the system?

---

## 2. Conceptual Database Design

A high-level representation of the database is created using the ER Model.

### Characteristics

* Independent of any DBMS
* Easy to understand
* Represents real-world objects

### Output

ER Diagram

---

## 3. Logical Database Design

The conceptual design is transformed into tables.

### Tasks

* Create tables
* Define attributes
* Assign primary keys
* Define foreign keys
* Apply normalization

---

## 4. Physical Database Design

Focuses on how data will actually be stored.

### Includes

* Storage organization
* Indexes
* Access paths
* Performance optimization

---

# Relational Modeling

The relational model stores data in tables called relations.

---

## Relation

A relation is a table made up of rows and columns.

### Example

| StudentID | Name  | Major |
| --------- | ----- | ----- |
| 101       | Sonam | IT    |
| 102       | Karma | CS    |

---

## Tuple

A tuple represents a row in a table.

Example:

```text
(101, Sonam, IT)
```

---

## Attribute

An attribute is a column in a relation.

Examples:

* StudentID
* Name
* Major

---

## Domain

A domain defines the permitted values for an attribute.

Examples:

* Age: 0–120
* Gender: Male, Female

---

## Properties of Relations

* Each row must be unique.
* Duplicate records are not allowed.
* Row order does not matter.
* Column order does not matter.
* Each cell contains a single value.
* Every attribute has a defined domain.

---

# Entity–Relationship (ER) Model

The ER Model is used to represent data conceptually before creating actual tables.

The main components are:

* Entities
* Attributes
* Relationships

---

## Entity

An entity is any real-world object about which information is stored.

### Examples

* Student
* Course
* Instructor
* Department

---

## Entity Set

An entity set is a collection of similar entities.

Example:

All students in a university.

---

## Attribute

Attributes describe the characteristics of an entity.

Examples:

| Attribute |
| --------- |
| StudentID |
| Name      |
| Address   |
| Age       |

---

## Relationship

A relationship shows how entities are connected.

Example:

```text
Student Enrolls in Course
```

---

## Simple ER Diagram

```text
Student
   |
 Enrolls
   |
Course
```

---

# Types of Attributes

Different attributes serve different purposes in a database.

---

## Simple Attribute

Cannot be divided into smaller parts.

Examples:

* Age
* Salary
* Gender

---

## Composite Attribute

Can be broken into smaller components.

### Example

```text
Name
 ├─ First Name
 ├─ Middle Name
 └─ Last Name
```

Another example:

```text
Address
 ├─ City
 ├─ State
 └─ Country
```

---

## Single-Valued Attribute

Contains only one value.

Examples:

* StudentID
* Date of Birth

---

## Multi-Valued Attribute

Contains multiple values.

Example:

A student may have several phone numbers.

---

## Derived Attribute

Calculated from another attribute.

Example:

Age derived from Date of Birth.

---

## Stored Attribute

Physically stored in the database.

Example:

Date of Birth.

---

## Key Attribute

Used to uniquely identify an entity.

Example:

StudentID.

---

# Keys in Database Design

Keys help uniquely identify records and establish relationships.

---

## Super Key

A set of attributes capable of uniquely identifying a record.

Examples:

* StudentID
* StudentID + Name

---

## Candidate Key

A minimal super key.

Examples:

* StudentID
* Email

---

## Primary Key

The chosen candidate key used as the main identifier.

### Features

* Unique
* Cannot be NULL

Example:

StudentID

---

## Alternate Key

Candidate keys that are not selected as the primary key.

Example:

Email

---

## Foreign Key

An attribute that references the primary key of another table.

### Example

Student Table:

| StudentID | Name | DepartmentID |

Department Table:

| DepartmentID | DepartmentName |

DepartmentID in the Student table acts as a foreign key.

---

# Relationship Types

Relationships describe how entities interact.

---

## One-to-One (1:1)

One entity is associated with only one other entity.

Example:

```text
Person ↔ Passport
```

One person has one passport.

---

## One-to-Many (1:M)

One entity can be associated with many entities.

Example:

```text
Department → Employees
```

One department may have many employees.

---

## Many-to-Many (M:N)

Many entities can be associated with many other entities.

Example:

```text
Students ↔ Courses
```

Students can enroll in multiple courses, and courses can contain multiple students.

---

## Cardinality Constraints

Cardinality specifies the number of entities involved in a relationship.

Types:

* 1:1
* 1:M
* M:N

---

## Participation Constraints

### Total Participation

Every entity must participate.

Example:

Every student belongs to a department.

### Partial Participation

Participation is optional.

Example:

Not every employee manages a project.

---

# Weak Entities

A weak entity cannot be uniquely identified using its own attributes.

It depends on another entity for identification.

### Example

Strong Entity:

* Employee

Weak Entity:

* Dependent

Relationship:

```text
Employee
    |
   Has
    |
Dependent
```

The dependent entity cannot exist without the employee.

---

# ER Diagram Symbols

| Symbol               | Meaning                |
| -------------------- | ---------------------- |
| Rectangle            | Entity                 |
| Diamond              | Relationship           |
| Oval                 | Attribute              |
| Double Oval          | Multi-Valued Attribute |
| Dashed Oval          | Derived Attribute      |
| Underlined Attribute | Key Attribute          |
| Double Rectangle     | Weak Entity            |

---

# Converting ER Diagrams into Relational Schemas

After creating an ER diagram, it must be converted into tables.

### ER Model

```text
Student
   |
 Enrolls
   |
Course
```

### Relational Schema

```text
Student(StudentID, Name)

Course(CourseID, CourseName)

Enrollment(StudentID, CourseID)
```

The Enrollment table represents the relationship between students and courses.

---

# Quick Revision Notes

* Database design reduces redundancy.
* Four design stages:

  * Requirements Collection
  * Conceptual Design
  * Logical Design
  * Physical Design
* Main ER Components:

  * Entity
  * Attribute
  * Relationship
* Important Keys:

  * Primary Key
  * Candidate Key
  * Foreign Key
* Relationship Types:

  * 1:1
  * 1:M
  * M:N
* Weak entities depend on strong entities.

---

# Unit Summary

This unit introduced the principles of database design and explained the stages involved in developing a database. It covered relational modeling concepts such as relations, tuples, attributes, and domains. The unit also discussed entities, relationships, keys, ER diagrams, weak entities, and the process of converting ER models into relational schemas. These concepts provide the foundation for designing efficient and well-structured databases.
