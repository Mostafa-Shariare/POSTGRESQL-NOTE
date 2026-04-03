# 📘 PostgreSQL Table Operations (CRUD Practice)

## 📌 1. Introduction

This document demonstrates basic **table operations (CRUD)** in PostgreSQL using the `psql` shell.

CRUD stands for:

* **C** → Create
* **R** → Read
* **U** → Update
* **D** → Delete

---

## 🏗️ 2. Creating a Table

```sql
CREATE TABLE person(
    id INT,
    name VARCHAR(100),
    city VARCHAR(100)
);
```

### 🔹 Description:

* Creates a table named `person`
* Defines three columns: `id`, `name`, `city`

---

## 🔍 3. Viewing Table Structure

```sql
\d person
```

### 🔹 Description:

Displays table schema (columns, data types, constraints)

---

## ➕ 4. Inserting Data

### 🔹 Single Row Insert

```sql
INSERT INTO person(id, name, city)
VALUES (101, 'Raju', 'Dhaka');
```

---

### 🔹 Multiple Row Insert

```sql
INSERT INTO person(id, name, city)
VALUES 
(101, 'Raju', 'Dhaka'),
(102, 'Rahim', 'Bogura');
```

---

### 🔹 Insert Without Column Names

```sql
INSERT INTO person
VALUES 
(101, 'Raju', 'Dhaka'),
(102, 'Rahim', 'Bogura');
```

---

## 📖 5. Reading Data

### 🔹 Select All Data

```sql
SELECT * FROM person;
```

---

### 🔹 Select Specific Columns

```sql
SELECT name, city FROM person;
```

---

## ✏️ 6. Updating Data

```sql
UPDATE person
SET city = 'Rajshahi'
WHERE name = 'Rahim';
```

### 🔹 Description:

* Updates city for rows where name = 'Rahim'

---

## ❗ Important Note:

If you forget `WHERE`:

```sql
UPDATE person SET city = 'Rajshahi';
```

👉 This will update **ALL rows** ⚠️

---

## ❌ 7. Deleting Data

```sql
DELETE FROM person
WHERE id = 101;
```

### 🔹 Description:

* Deletes rows where `id = 101`

---

## ❗ Important Note:

```sql
DELETE FROM person;
```

👉 Deletes **ALL data** but keeps the table

---

## 🚨 8. Comment Syntax Issue

You used:

```sql
# inserting data in the table
```

❌ This is **NOT valid in PostgreSQL**

✅ Correct:

```sql
-- inserting data in the table
```

---

## 🧠 9. Summary

| Operation    | Command        |
| ------------ | -------------- |
| Create Table | `CREATE TABLE` |
| Insert Data  | `INSERT INTO`  |
| Read Data    | `SELECT`       |
| Update Data  | `UPDATE`       |
| Delete Data  | `DELETE`       |

