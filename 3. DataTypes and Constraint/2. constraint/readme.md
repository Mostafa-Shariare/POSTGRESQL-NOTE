# 📘 Table Constraints in PostgreSQL

## 📌 1. Introduction

In PostgreSQL, **constraints** are rules applied to table columns to enforce data integrity and consistency.

They ensure that only **valid and reliable data** is stored in the database.

---

## 🧱 2. Primary Key Constraint

### 🔹 Definition

A **PRIMARY KEY** is a constraint that uniquely identifies each record (row) in a table.

### 🔹 Characteristics

* Each value must be **unique** ✅
* Cannot contain **NULL values** ❌
* A table can have **only one primary key**
* Automatically creates a **unique index**

---

### 🔹 Example

```sql
CREATE TABLE person (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(100)
);
```

---

### 🔹 Explanation

* `id` uniquely identifies each row
* No duplicate or null values are allowed

---

## 🚫 3. NOT NULL Constraint

### 🔹 Definition

The **NOT NULL** constraint ensures that a column cannot store `NULL` (empty) values.

---

### 🔹 Example

```sql
CREATE TABLE person (
    id INT,
    name VARCHAR(100) NOT NULL,
    city VARCHAR(100)
);
```

---

### 🔹 Explanation

* Every row **must have a value** for `name`
* Missing values will result in an error

---

## 🎯 4. DEFAULT Constraint

### 🔹 Definition

The **DEFAULT** constraint assigns a predefined value to a column when no value is provided during insertion.

---

### 🔹 Example

```sql
CREATE TABLE person (
    id INT,
    name VARCHAR(100),
    city VARCHAR(100) DEFAULT 'Dhaka'
);
```

---

### 🔹 Behavior

```sql
INSERT INTO person (id, name)
VALUES (101, 'Rahim');
```

👉 Result:

```text
city = 'Dhaka'
```

---

## 🔢 5. AUTO-INCREMENT (SERIAL)

### 🔹 Definition

PostgreSQL does not use the keyword “auto-increment” directly.
Instead, it provides **`SERIAL`** (or `BIGSERIAL`) to automatically generate sequential values.

---

### 🔹 Example

```sql
CREATE TABLE person (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(100)
);
```

---

### 🔹 Explanation

* `SERIAL` automatically:

  * Creates a sequence
  * Assigns increasing values (1, 2, 3, ...)
* No need to manually insert `id`

---

### 🔹 Example Insert

```sql
INSERT INTO person (name, city)
VALUES ('Rahim', 'Bogura');
```

👉 Result:

```text
id = 1 (automatically assigned)
```

---

## ⚖️ 6. Summary of Constraints

| Constraint  | Purpose                         |
| ----------- | ------------------------------- |
| PRIMARY KEY | Uniquely identifies each record |
| NOT NULL    | Prevents empty values           |
| DEFAULT     | Assigns default value           |
| SERIAL      | Auto-generates numeric values   |

---

