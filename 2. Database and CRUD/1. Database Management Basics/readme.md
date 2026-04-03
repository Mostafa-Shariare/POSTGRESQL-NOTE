
# 📘 PostgreSQL Practice Documentation (Database Operations)

## 📌 1. Introduction

This document summarizes basic database-level operations performed using the `psql` shell in PostgreSQL. These commands are essential for managing databases, switching between them, and performing administrative tasks.

---

## 📂 2. Listing All Databases

### 🔹 Command:

```sql id="c1a9dx"
\l
```

### 🔹 Description:

Displays a list of all databases available in the PostgreSQL server, including owner, encoding, and access privileges.

---

## 🔍 3. Viewing Database Names Using SQL

### 🔹 Command:

```sql id="m8x4qp"
SELECT datname FROM pg_database;
```

### 🔹 Description:

* Retrieves all database names from the system catalog table `pg_database`
* This is a SQL-based alternative to `\l`

---

## 🏗️ 4. Creating a New Database

### 🔹 Command:

```sql id="r2h6zs"
CREATE DATABASE test2;
```

### 🔹 Description:

Creates a new database named `test2`.

---

## 📂 5. Verifying Database Creation

### 🔹 Command:

```sql id="z0h7gf"
\l
```

### 🔹 Description:

Used again to confirm that `test2` has been successfully created.

---

## 🔌 6. Connecting to a Database

### 🔹 Command:

```sql id="g4k9wd"
\c test2
```

### 🔹 Description:

* Connects the current session to the `test2` database
* Required before performing operations inside that database

---

## ❌ 7. Dropping (Deleting) a Database

### 🔹 Command:

```sql id="v8n2qs"
DROP DATABASE test;
```

### 🔹 Description:

* Permanently deletes the database named `test`

### ⚠️ Important Notes:

* You **cannot drop a database you are currently connected to**
* Make sure to switch to another database before executing this command

---

## 🔁 8. Summary Workflow

```sql id="7w3xjf"
\l
SELECT datname FROM pg_database;
CREATE DATABASE test2;
\l
\c test2
DROP DATABASE test;
```

### 🔹 What You Learned:

* How to list databases (two methods)
* How to create a new database
* How to connect to a database
* How to delete a database safely

---

## 🧠 9. Key Takeaways

* `\l` → Quick overview of databases
* `pg_database` → System table storing database info
* Always verify actions using `\l`
* Be careful with `DROP DATABASE` (irreversible ⚠️)

---

## 📚 10. Conclusion

These commands form the foundation of database management in PostgreSQL. Mastering them is essential before moving to advanced topics like tables, schemas, and queries.

