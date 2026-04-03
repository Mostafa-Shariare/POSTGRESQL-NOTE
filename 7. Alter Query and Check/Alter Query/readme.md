
# 📘 ALTER TABLE in PostgreSQL (Schema Modification)

## 📌 1. Overview

In PostgreSQL, the `ALTER TABLE` statement is used to **modify the structure of an existing table**.

It allows changes such as:

* Adding or removing columns
* Modifying column definitions
* Renaming columns or tables
* Setting default values

These operations are essential for evolving database schemas without recreating tables.

---

## 🧱 2. Syntax

```sql
ALTER TABLE table_name
action;
```

Where `action` defines the type of modification.

---

## ➕ 3. Adding a New Column

### 🔹 Definition

Adds a new column to an existing table.

### 🔹 Example

```sql
ALTER TABLE employees
ADD COLUMN age INT;
```

---

## ❌ 4. Dropping a Column

### 🔹 Definition

Removes a column permanently from a table.

### 🔹 Example

```sql
ALTER TABLE employees
DROP COLUMN age;
```

### ⚠️ Note

* All data in the column will be lost permanently

---

## 🎯 5. Adding a Column with Default Value

### 🔹 Definition

Adds a column and assigns a default value for existing and future rows.

### 🔹 Example

```sql
ALTER TABLE employees
ADD COLUMN age INT DEFAULT 0;
```

---

## ✏️ 6. Renaming a Column

### 🔹 Definition

Changes the name of an existing column.

### 🔹 Example

```sql
ALTER TABLE employees
RENAME COLUMN age TO p_age;
```

---

## 🔁 7. Renaming a Table

### 🔹 Definition

Changes the name of an existing table.

---

### 🔹 Correct Syntax (PostgreSQL)

```sql
ALTER TABLE employees
RENAME TO person;
```

---

### ⚠️ Important Note

❌ This is **NOT valid in PostgreSQL**:

```sql
RENAME TABLE employees TO person;
```

👉 That syntax belongs to other database systems (e.g., MySQL)

---

## 🔧 8. Modifying Column Data Type

### 🔹 Definition

Changes the data type of a column.

### 🔹 Example

```sql
ALTER TABLE person
ALTER COLUMN fname
SET DATA TYPE VARCHAR(150);
```

---

### 🔹 Notes

* Existing data must be compatible with the new type
* Otherwise, PostgreSQL will raise an error

---

## 🧠 9. Summary of Operations

| Operation         | Command                      |
| ----------------- | ---------------------------- |
| Add Column        | `ADD COLUMN`                 |
| Drop Column       | `DROP COLUMN`                |
| Add Default Value | `DEFAULT`                    |
| Rename Column     | `RENAME COLUMN`              |
| Rename Table      | `RENAME TO`                  |
| Modify Data Type  | `ALTER COLUMN SET DATA TYPE` |

---

## ⚠️ 10. Important Considerations

* Schema changes may affect dependent objects (views, indexes, constraints)
* Dropping columns results in irreversible data loss
* Renaming operations do not affect data, only structure
* Always verify schema using:

```sql
\d table_name
```

---


