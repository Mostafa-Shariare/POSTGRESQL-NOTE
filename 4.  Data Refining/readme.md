# 📘 SQL Clauses Documentation (PostgreSQL)

## 📌 1. Overview

In PostgreSQL, SQL clauses are used in conjunction with statements such as `SELECT` to define conditions, control output, and manipulate the result set.

These clauses enable precise querying of relational data by allowing filtering, sorting, grouping, and limiting results.

---

## 🔍 2. WHERE Clause

### 2.1 Definition

The `WHERE` clause specifies conditions that must be satisfied for rows to be included in the result set.

### 2.2 Syntax

```sql
SELECT column_list
FROM table_name
WHERE condition;
```

---

### 2.3 Examples

#### a) Equality Condition

```sql
SELECT fname, email
FROM employees
WHERE emp_id = 6;
```

#### b) Comparison Operator

```sql
SELECT fname, email
FROM employees
WHERE salary > 3000;
```

#### c) Logical OR

```sql
SELECT fname, email
FROM employees
WHERE dept = 'HR' OR dept = 'Finance';
```

#### d) Logical AND

```sql
SELECT fname, email
FROM employees
WHERE dept = 'HR' AND salary > 30000;
```

---

## 📂 3. IN Clause

### 3.1 Definition

The `IN` clause is used to match a value against a list of possible values.

### 3.2 Syntax

```sql
SELECT column_list
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

### 3.3 Example

```sql
SELECT *
FROM employees
WHERE dept IN ('IT', 'HR', 'FINANCE');
```

---

## 📊 4. BETWEEN Clause

### 4.1 Definition

The `BETWEEN` clause filters values within a specified range (inclusive).

### 4.2 Syntax

```sql
SELECT column_list
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### 4.3 Example

```sql
SELECT fname, email
FROM employees
WHERE salary BETWEEN 3000 AND 50000;
```

---

## 🔁 5. DISTINCT Keyword

### 5.1 Definition

The `DISTINCT` keyword eliminates duplicate rows from the result set.

### 5.2 Syntax

```sql
SELECT DISTINCT column_name
FROM table_name;
```

### 5.3 Example

```sql
SELECT DISTINCT dept
FROM employees;
```

---

## 🔽 6. ORDER BY Clause

### 6.1 Definition

The `ORDER BY` clause sorts the result set based on one or more columns.

### 6.2 Syntax

```sql
SELECT column_list
FROM table_name
ORDER BY column_name [ASC | DESC];
```

---

### 6.3 Examples

#### a) Ascending Order (Default)

```sql
SELECT *
FROM employees
ORDER BY fname;
```

#### b) Descending Order

```sql
SELECT *
FROM employees
ORDER BY fname DESC;
```

---

## 🔢 7. LIMIT Clause

### 7.1 Definition

The `LIMIT` clause restricts the number of rows returned by a query.

### 7.2 Syntax

```sql
SELECT column_list
FROM table_name
LIMIT number;
```

### 7.3 Example

```sql
SELECT *
FROM employees
LIMIT 5;
```

---

## 🔎 8. LIKE Clause

### 8.1 Definition

The `LIKE` clause is used for pattern matching in string values.

---

### 8.2 Wildcards

| Symbol | Description                     |
| ------ | ------------------------------- |
| `%`    | Matches zero or more characters |
| `_`    | Matches exactly one character   |

---

### 8.3 Syntax

```sql
SELECT column_list
FROM table_name
WHERE column_name LIKE pattern;
```

---

### 8.4 Examples

#### a) Using `%` (Multiple Characters)

```sql
SELECT *
FROM employees
WHERE dept LIKE '%Acc%';
```

#### b) Using `_` (Single Character)

```sql
SELECT *
FROM employees
WHERE fname LIKE 'R_i%';
```

---

## ⚠️ 9. Important Notes

* String values must be enclosed in **single quotes (`'`)**
* SQL keywords are case-insensitive, but string matching may depend on collation
* `WHERE` clause conditions can be combined using `AND`, `OR`, and `NOT`
* `LIKE` is case-sensitive in PostgreSQL (use `ILIKE` for case-insensitive matching)

---

## 🧠 10. Conclusion

SQL clauses are fundamental components of query construction in PostgreSQL. Mastery of these clauses enables efficient data retrieval, filtering, and organization within relational databases.
