
# 📘 PostgreSQL Basic Commands (psql Shell)

## 📌 1. Introduction

`psql` is the interactive terminal-based interface for managing databases in PostgreSQL. It allows users to execute SQL queries, manage databases, and control database objects directly from the command line.

---

## ⚙️ 2. Starting psql

To connect to PostgreSQL using the default user (`postgres`):

```bash
psql -U postgres
```

### 🔹 Explanation:

* `-U` → Specifies the username
* `postgres` → Default superuser account

---

## 🧹 3. Clearing the Terminal Screen

```sql
\! cls
```

### 🔹 Explanation:

* `\!` → Executes a system (OS) command
* `cls` → Clears screen (Windows)

👉 For Linux/macOS:

```sql
\! clear
```

---

## 📂 4. Listing Databases

```sql
\l
```

### 🔹 Description:

Displays all available databases in PostgreSQL.

---

## 🏗️ 5. Creating a Database

```sql
CREATE DATABASE database_name;
```

### 🔹 Example:

```sql
CREATE DATABASE mydb;
```

---

## 🔌 6. Connecting to a Database

```sql
\c database_name
```

### 🔹 Example:

```sql
\c mydb
```

---

## 📋 7. Listing Tables

```sql
\dt
```

### 🔹 Description:

Shows all tables in the current database.

---

## 🧱 8. Creating a Table

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype
);
```

### 🔹 Example:

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

---

## ➕ 9. Inserting Data

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

### 🔹 Example:

```sql
INSERT INTO users (name, age)
VALUES ('John', 25);
```

---

## 🔍 10. Retrieving Data

```sql
SELECT * FROM table_name;
```

### 🔹 Example:

```sql
SELECT * FROM users;
```

---

## ❌ 11. Deleting a Database

```sql
DROP DATABASE database_name;
```

### ⚠️ Warning:

This permanently deletes the database.

---

## 🚪 12. Exiting psql

```sql
\q
```

---

## 🧠 13. Notes

* Commands starting with `\` are **psql meta-commands**
* SQL commands must end with a semicolon `;`
* PostgreSQL is **case-insensitive** by default for SQL keywords

---

## 📚 14. Conclusion

The `psql` shell provides a powerful interface for interacting with PostgreSQL databases. Understanding these basic commands is essential for database management, development, and debugging tasks.

