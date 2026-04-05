

# PostgreSQL Table Relationships – Detailed Documentation

Relational databases use **relationships** to define how tables are connected. These relationships ensure **data integrity, normalization, and proper querying**.

### Key Concepts

* **Primary Key (PK):**
  A column (or set of columns) that **uniquely identifies a row** in a table. Every table should have a PK.

* **Foreign Key (FK):**
  A column that **references the PK of another table** to establish a relationship. It ensures **referential integrity**, meaning data in the child table must correspond to existing data in the parent table.

* **Unique Constraint:**
  Ensures that values in a column or combination of columns are unique. Often used in **1:1 relationships**.

---

## 1. One-to-One Relationship (1:1)

### Definition

A **one-to-one relationship** exists when **each row in Table A corresponds to exactly one row in Table B**.

* Usually used to **split optional or sensitive data** into separate tables.
* Implemented with a **unique foreign key** in one of the tables.

### Real-World Example

**Scenario:** Each person has one passport.

**Tables:**

**person**

| person_id (PK) | name  | dob        |
| -------------- | ----- | ---------- |
| 1              | Alice | 1990-01-10 |
| 2              | Bob   | 1985-05-23 |

**passport**

| passport_id (PK) | person_id (FK, UNIQUE) | passport_no |
| ---------------- | ---------------------- | ----------- |
| 101              | 1                      | P123456     |
| 102              | 2                      | P789012     |

### SQL Implementation

```sql
CREATE TABLE person (
    person_id SERIAL PRIMARY KEY,  -- PK uniquely identifies each person
    name VARCHAR(50),
    dob DATE
);

CREATE TABLE passport (
    passport_id SERIAL PRIMARY KEY,           -- PK uniquely identifies each passport
    person_id INT UNIQUE REFERENCES person(person_id),  -- FK + UNIQUE enforces 1:1 mapping
    passport_no VARCHAR(20)
);
```

### Explanation

1. **person_id in `person`** is PK → each person is unique.
2. **person_id in `passport`** is FK referencing `person(person_id)` → ensures that every passport belongs to a valid person.
3. **UNIQUE constraint on person_id in passport** → prevents multiple passports for the same person.
4. Result → **exactly one passport per person**.

---

## 2. One-to-Many Relationship (1:N)

### Definition

A **one-to-many relationship** exists when **one row in Table A relates to multiple rows in Table B**, but each row in Table B relates to only one row in Table A.

* Most common relationship in databases.
* Implemented using a **foreign key in the “many” table**.

### Real-World Example

**Scenario:** A teacher can teach multiple courses, but each course is taught by only one teacher.

**Tables:**

**teacher**

| teacher_id (PK) | name       |
| --------------- | ---------- |
| 1               | Mrs. Smith |
| 2               | Mr. Brown  |

**course**

| course_id (PK) | course_name | teacher_id (FK) |
| -------------- | ----------- | --------------- |
| 101            | Math        | 1               |
| 102            | Physics     | 1               |
| 103            | Chemistry   | 2               |

### SQL Implementation

```sql
CREATE TABLE teacher (
    teacher_id SERIAL PRIMARY KEY,  -- PK uniquely identifies each teacher
    name VARCHAR(50)
);

CREATE TABLE course (
    course_id SERIAL PRIMARY KEY,    -- PK uniquely identifies each course
    course_name VARCHAR(50),
    teacher_id INT REFERENCES teacher(teacher_id)  -- FK links course to its teacher
);
```

### Explanation

1. `teacher_id` in `teacher` is PK → identifies each teacher uniquely.
2. `teacher_id` in `course` is FK → each course references a valid teacher.
3. A teacher can teach multiple courses → 1:N relationship.
4. Integrity → cannot assign a course to a non-existent teacher.

---

## 3. Many-to-Many Relationship (M:N)

### Definition

A **many-to-many relationship** exists when **multiple rows in Table A relate to multiple rows in Table B**.

* Implemented via a **junction (bridge) table** that holds foreign keys referencing both tables.
* The junction table often has a **composite primary key** to ensure uniqueness.

### Real-World Example

**Scenario:** Students can enroll in multiple courses, and each course can have multiple students.

**Tables:**

**student**

| student_id (PK) | name  |
| --------------- | ----- |
| 1               | Alice |
| 2               | Bob   |

**course**

| course_id (PK) | course_name |
| -------------- | ----------- |
| 101            | Math        |
| 102            | Physics     |

**student_course** (junction table)

| student_id (FK) | course_id (FK) | PRIMARY KEY(student_id, course_id) |
| --------------- | -------------- | ---------------------------------- |
| 1               | 101            | yes                                |
| 1               | 102            | yes                                |
| 2               | 101            | yes                                |

### SQL Implementation

```sql
CREATE TABLE student (
    student_id SERIAL PRIMARY KEY,  -- PK identifies each student
    name VARCHAR(50)
);

CREATE TABLE course (
    course_id SERIAL PRIMARY KEY,  -- PK identifies each course
    course_name VARCHAR(50)
);

CREATE TABLE student_course (
    student_id INT REFERENCES student(student_id),  -- FK → links to student
    course_id INT REFERENCES course(course_id),     -- FK → links to course
    PRIMARY KEY (student_id, course_id)            -- composite PK ensures uniqueness
);
```

### Explanation

1. `student_id` in `student` and `course_id` in `course` are PKs.
2. `student_course` contains **two FKs** referencing both tables.
3. **Composite PK `(student_id, course_id)`** prevents duplicate enrollment records.
4. Supports multiple students per course and multiple courses per student → M:N relationship.

---

## Summary Table with Keys

| Relationship | Parent Table PK       | Child/Junction Table PK       | Foreign Key               | Notes                                   |
| ------------ | --------------------- | ----------------------------- | ------------------------- | --------------------------------------- |
| 1:1          | person_id             | passport_id                   | person_id (UNIQUE FK)     | Each person has exactly one passport    |
| 1:N          | teacher_id            | course_id                     | teacher_id FK             | One teacher can teach multiple courses  |
| M:N          | student_id, course_id | student_course (composite PK) | student_id + course_id FK | Students can enroll in multiple courses |

---

## Best Practices

1. Always define **Primary Keys** for uniqueness.
2. Use **Foreign Keys** for referential integrity.
3. **1:1** → use UNIQUE FK.
4. **M:N** → always use a junction table with **composite PK**.
5. Index FK columns for performance on large datasets.
6. Avoid overlapping relationships that violate data integrity.


