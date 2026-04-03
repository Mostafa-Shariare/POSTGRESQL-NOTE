# 📘 Database vs Schema vs Table (PostgreSQL)

## 📌 1. Introduction

In PostgreSQL, data is organized in a hierarchical structure. The three core components of this structure are:

* **Database**
* **Schema**
* **Table**

Understanding their relationship is essential for designing and managing data efficiently.

---

## 🏢 2. What is a Database?

A **database** is the **top-level container** that stores all data and objects.

### 🔹 Key Features:

* Contains schemas, tables, views, functions, etc.
* Each database is isolated from others
* You must connect to a database before accessing data

### 🔹 Example:

```sql
CREATE DATABASE university;
```

👉 Think of a database like a **building** 🏢

---

## 🗂️ 3. What is a Schema?

A **schema** is a **logical grouping of database objects** inside a database.

### 🔹 Key Features:

* Organizes tables and other objects
* Helps avoid naming conflicts
* A database can have multiple schemas

### 🔹 Default Schema:

* `public` (automatically created in PostgreSQL)

### 🔹 Example:

```sql
CREATE SCHEMA academics;
```

👉 Think of a schema like a **floor inside a building** 🏬

---

## 📊 4. What is a Table?

A **table** is where the **actual data is stored** in rows and columns.

### 🔹 Key Features:

* Contains records (rows) and attributes (columns)
* Belongs to a specific schema
* Used to store structured data

### 🔹 Example:

```sql
CREATE TABLE academics.students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```

👉 Think of a table like a **room storing files** 📁

---

## 🔗 5. Relationship Between Them

Hierarchy:

```
Database
   └── Schema
         └── Table
```

### 🔹 Real Example:

```sql
university (Database)
   └── academics (Schema)
         └── students (Table)
```

---

## ⚖️ 6. Key Differences

| Feature   | Database 🏢    | Schema 🗂️       | Table 📊          |
| --------- | -------------- | ---------------- | ----------------- |
| Level     | Highest        | Middle           | Lowest            |
| Purpose   | Store all data | Organize objects | Store actual data |
| Contains  | Schemas        | Tables, views    | Rows & columns    |
| Isolation | Fully separate | Logical grouping | Data container    |

---

## 🧠 7. Why This Structure Matters

* ✅ Better organization of large systems
* ✅ Easier access control (permissions per schema)
* ✅ Avoid naming conflicts (same table name in different schemas)
* ✅ Improves maintainability

---

