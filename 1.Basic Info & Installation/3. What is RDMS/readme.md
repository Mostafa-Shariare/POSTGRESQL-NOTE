# What is RDBMS?

**RDBMS (Relational Database Management System)** is a type of database management system that stores data in **tables** and allows relationships between those tables.

In an RDBMS, data is organized using **rows** and **columns**.

* **Row** → represents a single record
* **Column** → represents a field or attribute

---

## Example Table

| First Name | Last Name | City   | Contact  |
| ---------- | --------- | ------ | -------- |
| Paul       | Philips   | London | 39899829 |
| Raju       | Sharma    | Ranchi | 90890288 |
| Keto       | Leri      | Tokyo  | 50505005 |
| Sham       | Sha       | Delhi  | 602020   |

Each row represents a **person**, and each column represents a **type of information**.

---

## Relationships in RDBMS

RDBMS allows multiple tables to be connected using **keys**:

* **Primary Key** → uniquely identifies each record in a table
* **Foreign Key** → connects one table with another table

Example:

### Students Table

| StudentID | Name |
| --------- | ---- |
| 1         | Paul |
| 2         | Raju |

### Courses Table

| StudentID | Course     |
| --------- | ---------- |
| 1         | Database   |
| 2         | Algorithms |

Here, **StudentID** connects the two tables, creating a **relationship**.

---

## Examples of RDBMS

Some popular relational database systems include:

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server

---

## Simple Definition

**RDBMS is a database management system that stores data in tables and connects those tables using relationships.**
