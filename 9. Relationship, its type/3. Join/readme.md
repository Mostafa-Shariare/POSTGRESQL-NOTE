# SQL JOINs – Detailed Explanation

## 1. Introduction

In relational databases, **JOINs** allow you to **combine rows from multiple tables** based on related columns. This is essential when data is normalized (split across tables).

* **Primary Key (PK):** Unique identifier for each row (e.g., `cust_id` in `customers`)
* **Foreign Key (FK):** Column in one table referencing PK in another (e.g., `cust_id` in `oders`)

Your tables:

```sql
CREATE TABLE customers(
    cust_id serial PRIMARY KEY,
    cust_name varchar(100) NOT NULL
);

CREATE TABLE oders(
    oder_id serial PRIMARY KEY,
    order_date date NOT NULL,
    price numeric NOT NULL,
    cust_id integer NOT NULL,
    FOREIGN KEY(cust_id) REFERENCES customers(cust_id)
);
```

---

## 2. Cross Join

**Definition:** Returns the **Cartesian product** of two tables. Every row in the first table is paired with every row in the second table.

**Use Case:** Rarely used, mainly for generating all combinations.

**Example:**

```sql
SELECT * FROM customers CROSS JOIN oders;
```

**Output:**
All customers × all orders.

* Alice paired with every order, Bob with every order, etc.
* Total rows = `number_of_customers × number_of_orders`.

---

## 3. Inner Join

**Definition:** Returns **only the rows where there is a match in both tables** based on a related column.

**Use Case:** Most common JOIN, to get related data.

**Syntax:**

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

**Example 1 – All matched rows:**

```sql
SELECT *
FROM customers AS c
INNER JOIN oders AS o
ON c.cust_id = o.cust_id;
```

**Output:**
Only orders that have a valid customer. Customers with no orders are excluded.

**Example 2 – Count orders per customer:**

```sql
SELECT c.cust_name, COUNT(o.oder_id)
FROM customers AS c
INNER JOIN oders AS o
ON c.cust_id = o.cust_id
GROUP BY c.cust_name;
```

**Output:**
Shows how many orders each customer made.

**Example 3 – Count and sum of orders per customer:**

```sql
SELECT c.cust_name, COUNT(o.oder_id), SUM(o.price)
FROM customers AS c
INNER JOIN oders AS o
ON c.cust_id = o.cust_id
GROUP BY c.cust_name;
```

**Output:**

* `count` → total orders per customer
* `sum` → total spending per customer

---

## 4. Left Join

**Definition:** Returns **all rows from the left table** (here `customers`) and **matched rows from the right table** (`oders`).

* If no match exists, right table columns are `NULL`.

**Use Case:** Get all customers including those who haven’t made any orders.

**Example:**

```sql
SELECT c.cust_name, o.oder_id, o.price
FROM customers AS c
LEFT JOIN oders AS o
ON c.cust_id = o.cust_id;
```

**Output:**

* Shows all customers.
* Customers without orders will have `NULL` for `oder_id` and `price`.

---

## 5. Right Join

**Definition:** Returns **all rows from the right table** (`oders`) and matched rows from the left table (`customers`).

* If no match exists, left table columns are `NULL`.

**Use Case:** Get all orders even if the customer record is missing (rare in properly normalized databases).

**Example:**

```sql
SELECT c.cust_name, o.oder_id, o.price
FROM customers AS c
RIGHT JOIN oders AS o
ON c.cust_id = o.cust_id;
```

**Output:**

* Shows all orders.
* If an order had no valid customer, `cust_name` would be `NULL`.

---

## 6. Summary Table

| JOIN Type  | Description                                       | Example Use Case                                                            |
| ---------- | ------------------------------------------------- | --------------------------------------------------------------------------- |
| CROSS JOIN | Cartesian product                                 | Testing all combinations                                                    |
| INNER JOIN | Only rows with matches in both tables             | Orders with valid customers                                                 |
| LEFT JOIN  | All rows from left table, matched rows from right | Show all customers and their orders (include those without orders)          |
| RIGHT JOIN | All rows from right table, matched rows from left | Show all orders and their customers (include orders with missing customers) |

---

## 7. Key Points

1. **JOIN condition (`ON`) is mandatory** for INNER, LEFT, RIGHT JOIN to specify how tables are related.
2. **GROUP BY** is often used with JOIN to aggregate data.
3. **NULL values** appear in LEFT/RIGHT JOIN when there’s no match.
4. **Aliases** (`AS c`, `AS o`) improve readability.

