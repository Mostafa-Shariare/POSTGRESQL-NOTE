

# 📘 String Functions in PostgreSQL

## 📌 1. Overview

In PostgreSQL, **string functions** are used to manipulate and process textual (character) data stored in database columns.

These functions support operations such as:

* Concatenation
* Extraction
* Transformation
* Formatting
* Searching

They are widely used in data cleaning, formatting output, and query customization.

---

## 🔹 2. Concatenation Functions

### 2.1 `CONCAT()`

#### 🔹 Definition

Combines two or more strings into a single string.

#### 🔹 Syntax

```sql
CONCAT(string1, string2, ...);
```

---

### 🔹 Examples

```sql
SELECT CONCAT(fname, lname) FROM employees;
```

```sql
SELECT CONCAT(fname, lname) AS fullname FROM employees;
```

```sql
SELECT emp_id, CONCAT(fname, ' ', lname) AS fullname FROM employees;
```

#### 🔹 Description

* Joins first name and last name
* Space can be added manually between values

---

### 2.2 `CONCAT_WS()` (Concatenate With Separator)

#### 🔹 Definition

Concatenates strings using a specified separator.

#### 🔹 Syntax

```sql
CONCAT_WS(separator, string1, string2, ...);
```

---

### 🔹 Example

```sql
SELECT emp_id, CONCAT_WS(' ', fname, lname) AS fullname FROM employees;
```

```sql
SELECT CONCAT_WS(':', fname, lname, dept) FROM employees;
```

#### 🔹 Description

* Automatically inserts the separator between values
* Ignores NULL values

---

## ✂️ 3. Substring Function

### 🔹 Function: `SUBSTR()` / `SUBSTRING()`

#### 🔹 Definition

Extracts a portion of a string starting from a given position.

#### 🔹 Syntax

```sql
SUBSTR(string, start, length);
```

---

### 🔹 Example

```sql
SELECT SUBSTR('Hello Buddy', 1, 6);
```

#### 🔹 Result:

```text
Hello 
```

---

## 🔁 4. Replace Function

### 🔹 Function: `REPLACE()`

#### 🔹 Definition

Replaces all occurrences of a substring within a string.

#### 🔹 Syntax

```sql
REPLACE(string, from_substring, to_substring);
```

---

### 🔹 Examples

```sql
SELECT REPLACE('abcxyd', 'abc', '123');
```

```sql
SELECT REPLACE(dept, 'IT', 'Tech') FROM employees;
```

---

## 🔄 5. Reverse Function

### 🔹 Function: `REVERSE()`

#### 🔹 Definition

Reverses the order of characters in a string.

---

### 🔹 Example

```sql
SELECT REVERSE(fname) FROM employees;
```

---

## 📏 6. Length Function

### 🔹 Function: `LENGTH()`

#### 🔹 Definition

Returns the number of characters in a string.

---

### 🔹 Examples

```sql
SELECT LENGTH('Hello');
```

```sql
SELECT LENGTH(fname) FROM employees;
```

```sql
SELECT * FROM employees
WHERE LENGTH(fname) > 5;
```

---

## 🔠 7. Case Conversion Functions

### 7.1 `UPPER()`

#### 🔹 Definition

Converts all characters to uppercase.

```sql
SELECT UPPER(fname) FROM employees;
```

---

### 7.2 `LOWER()`

#### 🔹 Definition

Converts all characters to lowercase.

```sql
SELECT LOWER(fname) FROM employees;
```

---

## ✂️ 8. String Extraction Functions

### 8.1 `LEFT()`

#### 🔹 Definition

Returns the leftmost characters of a string.

```sql
SELECT LEFT(fname, 3) FROM employees;
```

---

### 8.2 `RIGHT()`

#### 🔹 Definition

Returns the rightmost characters of a string.

```sql
SELECT RIGHT(fname, 3) FROM employees;
```

---

## 🧹 9. TRIM Function

### 🔹 Function: `TRIM()`

#### 🔹 Definition

Removes leading and trailing spaces (or specified characters).

---

### 🔹 Example

```sql
SELECT TRIM('   Hello   ');
```

---

## 🔍 10. POSITION Function

### 🔹 Function: `POSITION()`

#### 🔹 Definition

Returns the position of a substring within a string.

---

### 🔹 Syntax

```sql
POSITION(substring IN string);
```

---

### 🔹 Example

```sql
SELECT POSITION('Buddy' IN 'Hello Buddy');
```

---

## 🧠 11. Practical Example

```sql
SELECT CONCAT_WS(':', fname, lname, dept)
FROM employees;
```

#### 🔹 Description

* Combines multiple columns into a formatted string
* Uses `:` as a separator

---

## ⚠️ 12. Important Notes

* String functions are **case-sensitive** in many operations
* Most functions ignore `NULL` values (e.g., `CONCAT_WS`)
* Indexing in substring functions starts from **1 (not 0)**
* Use appropriate functions for formatting and readability

---

