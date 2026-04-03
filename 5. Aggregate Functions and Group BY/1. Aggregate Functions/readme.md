# 📘 Aggregate Functions in PostgreSQL

## 📌 1. Overview

In PostgreSQL, **aggregate functions** perform calculations on a set of rows and return a **single summarized value**.

These functions are commonly used in data analysis to compute totals, averages, counts, and other statistical values.

---

## 🔹 2. Definition

An **aggregate function** operates on multiple rows of a column and produces a single output value.

---

## 🔢 3. Common Aggregate Functions

### 3.1 COUNT()

#### 🔹 Definition

Returns the number of rows that match a specified condition.

#### 🔹 Syntax

```sql
SELECT COUNT(column_name)
FROM table_name;
```

#### 🔹 Example

```sql
SELECT COUNT(*) FROM employees;
```

👉 Counts total number of records in the table

---

### 3.2 MIN()

#### 🔹 Definition

Returns the **smallest value** in a column.

#### 🔹 Syntax

```sql
SELECT MIN(column_name)
FROM table_name;
```

#### 🔹 Example

```sql
SELECT MIN(salary) FROM employees;
```

👉 Finds the lowest salary

---

### 3.3 MAX()

#### 🔹 Definition

Returns the **largest value** in a column.

#### 🔹 Syntax

```sql
SELECT MAX(column_name)
FROM table_name;
```

#### 🔹 Example

```sql
SELECT MAX(salary) FROM employees;
```

👉 Finds the highest salary

---

### 3.4 AVG()

#### 🔹 Definition

Calculates the **average (mean)** value of a column.

#### 🔹 Syntax

```sql
SELECT AVG(column_name)
FROM table_name;
```

#### 🔹 Example

```sql
SELECT AVG(salary) FROM employees;
```

👉 Returns average salary

---

### 3.5 SUM()

#### 🔹 Definition

Returns the **total sum** of a numeric column.

#### 🔹 Syntax

```sql
SELECT SUM(column_name)
FROM table_name;
```

#### 🔹 Example

```sql
SELECT SUM(salary) FROM employees;
```

👉 Calculates total salary of all employees

---

## 📊 4. Using Aggregate Functions with WHERE

Aggregate functions can be combined with filtering conditions.

### 🔹 Example

```sql
SELECT COUNT(*)
FROM employees
WHERE dept = 'IT';
```

👉 Counts employees in IT department

---

## 📂 5. Using Aggregate Functions with GROUP BY

### 🔹 Definition

`GROUP BY` groups rows that have the same values into summary rows.

---

### 🔹 Example

```sql
SELECT dept, AVG(salary)
FROM employees
GROUP BY dept;
```

👉 Shows average salary for each department

---

## ⚠️ 6. Important Notes

* Aggregate functions ignore **NULL values** (except `COUNT(*)`)
* They return a **single value per group**
* Often used with `GROUP BY` for categorized analysis
* Can be combined with `WHERE` for filtering

---

## ⚖️ 7. Summary Table

| Function | Description    |
| -------- | -------------- |
| COUNT()  | Counts rows    |
| MIN()    | Smallest value |
| MAX()    | Largest value  |
| AVG()    | Average value  |
| SUM()    | Total sum      |

---

## 🧠 8. Example Combined Query

```sql
SELECT dept,
       COUNT(*) AS total_employees,
       AVG(salary) AS avg_salary,
       MAX(salary) AS highest_salary,
       MIN(salary) AS lowest_salary
FROM employees
GROUP BY dept;
```

👉 Provides full summary statistics per department

---

## 📚 9. Conclusion

Aggregate functions are essential tools for summarizing and analyzing data in PostgreSQL. They enable efficient computation of key metrics across large datasets.

