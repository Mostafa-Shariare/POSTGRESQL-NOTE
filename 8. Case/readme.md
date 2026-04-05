

# PostgreSQL CASE Expression Documentation

## Overview

The `CASE` expression in PostgreSQL provides conditional logic within SQL queries. It allows you to evaluate conditions and return values dynamically, similar to `if-else` statements in programming languages.

It is commonly used for:

* Data categorization
* Conditional calculations
* Dynamic column generation
* Aggregation with conditions

---

## Syntax

```sql
CASE
    WHEN condition THEN result
    [WHEN ...]
    [ELSE result]
END
```

* `WHEN`: Specifies a condition
* `THEN`: Value returned if condition is true
* `ELSE`: Default value (optional)
* `END`: समाप्त (terminates the CASE expression)

---

## 1. Basic CASE Usage

### Example: Categorizing Salary (High / Low)

```sql
SELECT fname, salary,
CASE
    WHEN salary >= 50000 THEN 'High'
    ELSE 'Low'
END AS sal_cat
FROM person;
```

### Explanation

* If `salary >= 50000` → returns `'High'`
* Otherwise → returns `'Low'`
* Result is shown as a new column `sal_cat`

---

## 2. Multiple Conditions

### Example: High, Mid, Low Salary Classification

```sql
SELECT fname, salary,
CASE
    WHEN salary >= 50000 THEN 'High'
    WHEN salary >= 40000 AND salary < 50000 THEN 'Mid'
    ELSE 'Low'
END AS sal_cat
FROM person;
```

### Explanation

* Conditions are evaluated top to bottom
* First matching condition is executed
* Important: Order matters

---

## 3. Logical Range Handling

### Example (Potential Overlap Issue)

```sql
WHEN salary >= 50000 THEN 'High'
WHEN salary >= 40000 AND salary <= 50000 THEN 'Mid'
```

### Issue

* `salary = 50000` matches both conditions
* PostgreSQL will pick the **first match** (`High`)

### Best Practice

Avoid overlapping conditions:

```sql
WHEN salary >= 50000 THEN 'High'
WHEN salary >= 40000 THEN 'Mid'
```

---

## 4. CASE with Calculated Columns

### Example: Bonus Calculation

```sql
SELECT fname, salary,
CASE
    WHEN salary >= 50000 THEN 'High'
    WHEN salary >= 40000 AND salary <= 50000 THEN 'Mid'
    ELSE 'Low'
END AS sal_cat,

CASE
    WHEN salary > 0 THEN ROUND(salary * 0.10)
END AS bonus

FROM person;
```

### Explanation

* Adds a computed column `bonus`
* Calculates 10% of salary
* `ROUND()` is used to remove decimals
* If condition not met → returns `NULL`

---

## 5. CASE with Aggregation (GROUP BY)

### Problematic Query

```sql
SELECT
CASE
    WHEN salary >= 50000 THEN 'High'
    WHEN salary >= 40000 AND salary <= 50000 THEN 'Mid'
    ELSE 'Low'
END AS sal_cat, count(fname)
FROM person
GROUP BY sal_cat;
```

### Issue

* PostgreSQL does **not allow alias (`sal_cat`) in GROUP BY** in the same query level

---

## 6. Correct Approach Using Subquery

```sql
SELECT sal_cat, COUNT(fname)
FROM (
    SELECT fname, salary,
    CASE
        WHEN salary >= 50000 THEN 'High'
        WHEN salary >= 40000 THEN 'Mid'
        ELSE 'Low'
    END AS sal_cat
    FROM person
) AS sub
GROUP BY sal_cat;
```

### Explanation

* Inner query creates `sal_cat`
* Outer query performs aggregation
* This avoids alias limitations

---

## 7. Alternative Solution (Direct GROUP BY Expression)

PostgreSQL also allows repeating the expression:

```sql
SELECT
CASE
    WHEN salary >= 50000 THEN 'High'
    WHEN salary >= 40000 THEN 'Mid'
    ELSE 'Low'
END AS sal_cat,
COUNT(fname)
FROM person
GROUP BY
CASE
    WHEN salary >= 50000 THEN 'High'
    WHEN salary >= 40000 THEN 'Mid'
    ELSE 'Low'
END;
```

---

## Key Notes & Best Practices

* ✔ Always order conditions carefully (top → bottom)
* ✔ Avoid overlapping ranges
* ✔ Use `ELSE` to handle unexpected values
* ✔ Use subqueries when grouping by derived columns
* ✔ `CASE` returns `NULL` if no condition matches and no `ELSE` is provided

---

