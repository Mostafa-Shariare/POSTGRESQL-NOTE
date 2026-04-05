# 📘 Many-to-Many Relationship in PostgreSQL

## 🔹 What is Many-to-Many?

A **many-to-many (M:N)** relationship means:

* One record in Table A can relate to **multiple records** in Table B
* One record in Table B can relate to **multiple records** in Table A

👉 Example:

* A **student** can enroll in multiple **courses**
* A **course** can have multiple **students**

---

## 🔹 Problem

Relational databases **cannot directly represent many-to-many relationships**.

👉 Solution: Use a **junction table (bridge table)**

---

## 🔹 Database Design

### 1. Students Table

```sql
create table students(
    s_id serial primary key,
    name varchar(100) not null
);
```

### 2. Courses Table

```sql
create table courses (
    c_id serial primary key,
    name varchar(100) not null,
    fee numeric not null
);
```

### 3. Enrollment Table (Junction Table)

```sql
create table enrollment(
    enrollment_id serial primary key,
    s_id int not null,
    c_id int not null,
    enrollment_date date not null,
    foreign key(s_id) references students(s_id),
    foreign key(c_id) references courses(c_id)
);
```

---

## 🔹 Key Concepts

### ✅ Primary Key

* Uniquely identifies each row
* Example:

  * `students.s_id`
  * `courses.c_id`
  * `enrollment.enrollment_id`

### ✅ Foreign Key

* Creates relationship between tables
* Example:

  * `enrollment.s_id → students.s_id`
  * `enrollment.c_id → courses.c_id`

### ✅ Junction Table

* `enrollment` connects `students` and `courses`
* Each row = one relationship

---

## 🔹 Sample Data

### Students

| s_id | name    |
| ---- | ------- |
| 1    | Alice   |
| 2    | Bob     |
| 3    | Charlie |
| 4    | David   |
| 5    | Eve     |

---

### Courses

| c_id | name             | fee |
| ---- | ---------------- | --- |
| 1    | Mathematics      | 500 |
| 2    | Physics          | 600 |
| 3    | Chemistry        | 550 |
| 4    | Biology          | 450 |
| 5    | Computer Science | 700 |

---

### Enrollment (Bridge Table)

| enrollment_id | s_id | c_id | date       |
| ------------- | ---- | ---- | ---------- |
| 1             | 1    | 1    | 2024-01-10 |
| 2             | 1    | 5    | 2024-01-15 |
| ...           | ...  | ...  | ...        |

---

## 🔹 Basic JOIN Query

```sql
select s.name, c.name, e.enrollment_date, c.fee
from enrollment e
join students s on e.s_id = s.s_id
join courses c on c.c_id = e.c_id;
```

### 🔸 Output

| student | course           | date       | fee |
| ------- | ---------------- | ---------- | --- |
| Alice   | Mathematics      | 2024-01-10 | 500 |
| Alice   | Computer Science | 2024-01-15 | 700 |
| Bob     | Physics          | 2024-01-12 | 600 |
| ...     | ...              | ...        | ... |

---

# 🔹 More Useful Queries (Important 🔥)

## 1. 📌 Find all courses taken by a specific student

```sql
select c.name
from enrollment e
join courses c on e.c_id = c.c_id
where e.s_id = 1;
```

### Output (Alice)

| course           |
| ---------------- |
| Mathematics      |
| Computer Science |

---

## 2. 📌 Find all students in a specific course

```sql
select s.name
from enrollment e
join students s on e.s_id = s.s_id
where e.c_id = 1;
```

### Output (Mathematics)

| student |
| ------- |
| Alice   |
| Charlie |

---

## 3. 📌 Count students per course

```sql
select c.name, count(e.s_id) as total_students
from courses c
left join enrollment e on c.c_id = e.c_id
group by c.name;
```

### Output

| course           | total_students |
| ---------------- | -------------- |
| Mathematics      | 2              |
| Physics          | 2              |
| Chemistry        | 2              |
| Biology          | 2              |
| Computer Science | 2              |

---

## 4. 📌 Total fee paid by each student

```sql
select s.name, sum(c.fee) as total_fee
from students s
join enrollment e on s.s_id = e.s_id
join courses c on c.c_id = e.c_id
group by s.name;
```

### Output

| student | total_fee |
| ------- | --------- |
| Alice   | 1200      |
| Bob     | 1150      |
| Charlie | 950       |
| David   | 1250      |
| Eve     | 1050      |

---

## 5. 📌 Students enrolled in more than 1 course

```sql
select s.name, count(e.c_id) as total_courses
from students s
join enrollment e on s.s_id = e.s_id
group by s.name
having count(e.c_id) > 1;
```

---

## 6. 📌 Courses with fee greater than average

```sql
select name, fee
from courses
where fee > (select avg(fee) from courses);
```

---

# 🔹 Best Practices 💡

### ✔ Use composite unique constraint (important)

To prevent duplicate enrollments:

```sql
alter table enrollment
add constraint unique_enrollment unique (s_id, c_id);
```

---

### ✔ Use meaningful naming

* `students`, `courses`, `enrollment` ✔
* Avoid unclear names like `t1`, `t2`

---

### ✔ Normalize data

* Avoid storing course names in enrollment table
* Use IDs instead (you did it correctly 👍)

---

