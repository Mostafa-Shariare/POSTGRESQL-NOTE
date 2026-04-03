# SQL vs PostgreSQL

## What is SQL?

**SQL (Structured Query Language)** is a **language used to communicate with databases**.

It is used to:

* Create tables
* Insert data
* Update data
* Delete data
* Retrieve data

### Example SQL Query

```sql
SELECT * FROM users;
```

This query retrieves all records from the `users` table.

SQL is **not a database**. It is just a **language used to work with databases**.

---

## What is PostgreSQL?

PostgreSQL is a **Relational Database Management System (RDBMS)**.

It is software that stores and manages databases. PostgreSQL uses **SQL** to interact with the stored data.

PostgreSQL provides features such as:

* Data storage
* Query processing
* Security
* Data integrity
* Backup and recovery

---

## SQL vs PostgreSQL

| SQL                                      | PostgreSQL                         |
| ---------------------------------------- | ---------------------------------- |
| A query language                         | A database management system       |
| Used to interact with databases          | Used to store and manage databases |
| Standard language used by many databases | Specific database software         |
| Example: `SELECT`, `INSERT`, `UPDATE`    | Example: PostgreSQL server         |

---

## Simple Analogy

Think of it like this:

* **SQL → Language used to ask questions**
* **PostgreSQL → The database system that understands and executes those questions**

---

## Simple Definition

**SQL** is a language used to query and manage data in databases.
**PostgreSQL** is a database system that stores data and uses SQL for operations.
