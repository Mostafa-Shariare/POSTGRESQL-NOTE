
# **PostgreSQL Table Alteration and Constraint Management**

## **Overview**

This document describes how to modify an existing table in PostgreSQL using the `ALTER TABLE` statement, including adding columns, applying constraints, removing constraints, and defining named constraints.

---

## **1. Retrieving Data from a Table**

To view all records from a table:

```sql
SELECT * FROM person;
```

### Description

* `SELECT *` retrieves all columns.
* `person` is the target table.

---

## **2. Adding a New Column with Constraint**

A new column can be added using the `ALTER TABLE` statement along with constraints.

```sql
ALTER TABLE person
ADD COLUMN mob VARCHAR(15)
CHECK (LENGTH(mob) >= 10);
```

### Description

* `ADD COLUMN` adds a new field (`mob`) to the table.
* `VARCHAR(15)` defines the data type.
* `CHECK (LENGTH(mob) >= 10)` ensures that the value contains at least 10 characters.

### Behavior

* If inserted data violates the condition, PostgreSQL will reject the operation.
* Existing rows must satisfy the constraint (or be NULL if allowed).

---

## **3. Adding a Named Constraint**

Constraints can be explicitly named for easier management.

```sql
ALTER TABLE person
ADD CONSTRAINT person_mob_check
CHECK (LENGTH(mob) >= 10);
```

### Description

* `ADD CONSTRAINT` assigns a custom name (`person_mob_check`).
* Naming constraints improves readability and maintainability.

---

## **4. Dropping a Constraint**

To remove an existing constraint:

```sql
ALTER TABLE person
DROP CONSTRAINT person_mob_check;
```

### Description

* `DROP CONSTRAINT` removes the specified constraint.
* Requires the exact constraint name.

---

## **5. Adding a Constraint to an Existing Column**

If a column already exists, constraints can be added separately:

```sql
ALTER TABLE person
ADD CONSTRAINT person_mob_length_check
CHECK (LENGTH(mob) >= 10);
```

---

## **6. Best Practices**

* **Use Named Constraints**
  Always assign meaningful names to constraints for easier debugging and maintenance.

* **Validate Existing Data**
  Ensure existing records comply with new constraints before applying them.

* **Use CHECK for Data Validation**
  Suitable for enforcing business rules like length, ranges, or formats.

* **Keep Constraints Simple**
  Complex logic should be handled at the application level when necessary.

---

