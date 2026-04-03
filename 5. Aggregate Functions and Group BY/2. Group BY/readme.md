# 📘 GROUP BY Clause in PostgreSQL

## 📌 1. Overview

In PostgreSQL, the `GROUP BY` clause is used to **group rows that have the same values** in specified columns into summary rows.

It is commonly used with **aggregate functions** such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()`.

---

## 🔹 2. Definition

The `GROUP BY` clause groups rows based on one or more columns and allows aggregate functions to be applied to each group.

---

## 🔹 3. Syntax

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name;
```

---

## 🔹 4. Basic Examples

### 4.1 Grouping by Department

```sql
SELECT dept
FROM employees
GROUP BY dept;
```

👉 Returns unique departments (similar to `DISTINCT`)

---

### 4.2 Count Employees per Department

```sql
SELECT dept, COUNT(fname)
FROM employees
GROUP BY dept;
```

👉 Counts number of employees in each department

---

## 📊 5. More Examples

### 5.1 Average Salary per Department

```sql
SELECT dept, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept;
```

---

### 5.2 Total Salary per Department

```sql
SELECT dept, SUM(salary) AS total_salary
FROM employees
GROUP BY dept;
```

---

### 5.3 Maximum Salary per Department

```sql
SELECT dept, MAX(salary) AS highest_salary
FROM employees
GROUP BY dept;
```

---

### 5.4 Minimum Salary per Department

```sql
SELECT dept, MIN(salary) AS lowest_salary
FROM employees
GROUP BY dept;
```

---

### 5.5 Multiple Columns in GROUP BY

```sql
SELECT dept, hire_date, COUNT(*)
FROM employees
GROUP BY dept, hire_date;
```

👉 Groups data by both department and hire date

---

### 5.6 Using WHERE with GROUP BY

```sql
SELECT dept, COUNT(*)
FROM employees
WHERE salary > 30000
GROUP BY dept;
```

👉 Counts employees per department with salary greater than 30000

---

### 5.7 Using ORDER BY with GROUP BY

```sql
SELECT dept, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept
ORDER BY avg_salary DESC;
```

👉 Sorts departments by average salary (highest first)

---

## ⚠️ 6. Important Rules

* Every column in `SELECT` must be:

  * Either in `GROUP BY`
  * Or used with an aggregate function

❌ Invalid:

```sql
SELECT fname, dept FROM employees GROUP BY dept;
```

✔ Correct:

```sql
SELECT dept, COUNT(fname) FROM employees GROUP BY dept;
```

---

## 🔍 7. GROUP BY vs DISTINCT

| Feature     | GROUP BY          | DISTINCT          |
| ----------- | ----------------- | ----------------- |
| Purpose     | Group + aggregate | Remove duplicates |
| Aggregation | Yes               | No                |

---

## 🧠 8. Summary

* `GROUP BY` groups rows with same values
* Used with aggregate functions
* Helps in data summarization and analysis
* Can be combined with `WHERE` and `ORDER BY`

---

