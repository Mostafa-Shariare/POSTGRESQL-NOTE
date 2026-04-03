# 📘 Data Types in PostgreSQL (Column Attributes)

## 📌 1. Overview

In PostgreSQL, a **data type** is a fundamental attribute assigned to each column in a table. It defines the **kind of values** the column can store, how the data is interpreted, and what operations can be performed on it.

Every column in a relational table must have an explicitly defined data type. This ensures:

* **Data integrity** (only valid data is stored)
* **Type safety** (operations behave predictably)
* **Efficient storage and indexing**

---

## 🧱 2. Definition

A **data type** specifies:

* The **domain of values** allowed in a column
* The **format** of stored data
* The **set of valid operations** on that data

---

## 🔢 3. Commonly Used Data Types

### 3.1 Integer Types (`INT`)

The `INT` (or `INTEGER`) data type stores whole numbers without fractional components.

#### Characteristics:

* Supports positive and negative integers
* Does not allow decimal values
* Commonly used for identifiers and counts

#### Example:

```sql
id INT
```

---

### 3.2 Character Types (`VARCHAR`)

The `VARCHAR(n)` data type stores variable-length character strings.

#### Characteristics:

* Stores text data up to a maximum length `n`
* Efficient storage (only uses required space)
* Case-sensitive depending on collation

#### Example:

```sql
name VARCHAR(100)
```

---

### 3.3 Date Type (`DATE`)

The `DATE` data type stores calendar dates.

#### Characteristics:

* Format: `YYYY-MM-DD`
* Supports date operations (comparison, arithmetic)

#### Example:

```sql
dob DATE
```

---

### 3.4 Boolean Type (`BOOLEAN`)

The `BOOLEAN` data type represents logical values.

#### Allowed Values:

* `TRUE`
* `FALSE`
* `NULL` (unknown)

#### Example:

```sql
is_active BOOLEAN
```

---

## 🔍 4. Handling Decimal Values (Case Study: 11.35)

Consider inserting the value:

```text
11.35
```

The behavior depends on the column’s data type.

---

### 4.1 When Column Type is `INT`

```sql
age INT
```

#### Result:

* PostgreSQL raises an error:

  ```
  ERROR: invalid input syntax for type integer
  ```

#### Reason:

* `INT` only accepts whole numbers
* Fractional values violate the type constraint

---

### 4.2 When Column Type is `VARCHAR`

```sql
value VARCHAR(20)
```

#### Result:

* Value is stored as text:

  ```
  "11.35"
  ```

#### Note:

* No numeric operations can be performed unless converted

---

### 4.3 When Column Type is `FLOAT`

```sql
price FLOAT
```

#### Result:

* Value is stored approximately:

  ```
  11.35
  ```

#### Note:

* Floating-point types may introduce rounding errors

---

### 4.4 When Column Type is `NUMERIC` / `DECIMAL`

```sql
price NUMERIC(5,2)
```

#### Result:

* Value is stored precisely:

  ```
  11.35
  ```

#### Characteristics:

* Exact precision storage
* Recommended for financial data

---

## ⚖️ 5. Comparison of Data Types

| Data Type | Accepts Decimal | Storage Type | Use Case          |
| --------- | --------------- | ------------ | ----------------- |
| INT       | No              | Exact        | IDs, counts       |
| VARCHAR   | Yes (as text)   | Text         | Names, strings    |
| FLOAT     | Yes             | Approximate  | Scientific values |
| NUMERIC   | Yes             | Exact        | Financial data    |

---

## ⚠️ 6. Type Enforcement and Errors

PostgreSQL enforces strict type checking. If a value does not match the column’s data type:

* The operation is rejected
* An error is generated

Example:

```sql
INSERT INTO person(id) VALUES (11.35);
```

Result:

```
ERROR: invalid input syntax for type integer
```

---

## 🧠 7. Best Practices

* Use `INT` for whole numbers only
* Use `VARCHAR` for textual data
* Use `DATE` for date values instead of strings
* Use `BOOLEAN` for logical flags
* Use `NUMERIC` for precise decimal values (e.g., currency)
* Avoid using `FLOAT` when exact precision is required

---

## 📚 8. Conclusion

Data types play a critical role in database design. Proper selection of data types ensures:

* Data validity
* Accurate computations
* Efficient storage

Incorrect usage may lead to errors, data loss, or inaccurate results.

