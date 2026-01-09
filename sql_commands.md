
---

````md
# PostgreSQL Basic Commands — Step by Step (Beginner to Practical)

---

## Step 1️⃣ PostgreSQL-এ ঢোকা (psql)

```bash
psql -U postgres
````

---

## Step 2️⃣ Database তৈরি করা

### নতুন Database তৈরি

```sql
CREATE DATABASE company_db;
```

### Database list দেখো

```sql
\l
```

### Database ব্যবহার করা

```sql
\c company_db
```

---

## Step 3️⃣ Table তৈরি করা

ধরি, আমরা একটি **employee** টেবিল তৈরি করবো।

```sql
CREATE TABLE employee (
    id SERIAL PRIMARY KEY,
    employee_id INTEGER,
    name VARCHAR(50)
);
```

### Table list দেখো

```sql
\dt
```

### Table structure দেখো

```sql
\d employee
```

---

## Step 4️⃣ Table-এ Data Insert করা

### Single Row Insert

```sql
INSERT INTO employee (employee_id, name)
VALUES (4560, 'John');
```

### Multiple Row Insert

```sql
INSERT INTO employee (employee_id, name)
VALUES
(8962, 'Doe'),
(7788, 'Alex');
```

### Data দেখো

```sql
SELECT * FROM employee;
```

---

## Step 5️⃣ ALTER TABLE (Structure পরিবর্তন)

📌 **ALTER ব্যবহার করা হয় যখন table তৈরি হয়ে গেছে,
কিন্তু পরে structure পরিবর্তন দরকার হয়।**

---

### 🔹 5.1 Column ADD করা

```sql
ALTER TABLE employee
ADD COLUMN dob DATE;
```

```sql
SELECT * FROM employee;
```

---

### 🔹 5.2 Column DROP করা

```sql
ALTER TABLE employee
DROP COLUMN dob;
```

---

### 🔹 5.3 Column RENAME করা

```sql
ALTER TABLE employee
RENAME COLUMN name TO full_name;
```

---

### 🔹 5.4 Data Type পরিবর্তন করা

```sql
ALTER TABLE employee
ALTER COLUMN full_name
TYPE VARCHAR(25);
```

📌 ব্যবহার হবে যখন:

* আগে 50 ছিল
* পরে requirement অনুযায়ী 25 দরকার

---

### 🔹 5.5 Default Value সেট করা

```sql
ALTER TABLE employee
ALTER COLUMN employee_id
SET DEFAULT 1000;
```

---

### 🔹 5.6 Default Value DROP করা

```sql
ALTER TABLE employee
ALTER COLUMN employee_id
DROP DEFAULT;
```

---

### 🔹 5.7 Constraint ADD করা

```sql
ALTER TABLE employee
ADD CONSTRAINT emp_unique_id UNIQUE (employee_id);
```

---

### 🔹 5.8 Constraint DROP করা

```sql
ALTER TABLE employee
DROP CONSTRAINT emp_unique_id;
```

---

### 🔹 5.9 Table RENAME করা

```sql
ALTER TABLE employee
RENAME TO employees;
```

---

## Step 6️⃣ SELECT — Data Retrieve করা

### সব data

```sql
SELECT * FROM employees;
```

### নির্দিষ্ট column

```sql
SELECT full_name, employee_id FROM employees;
```

### WHERE ব্যবহার

```sql
SELECT * FROM employees
WHERE employee_id = 4560;
```

---

## Step 7️⃣ SELECT এর কিছু গুরুত্বপূর্ণ Option

### DISTINCT

```sql
SELECT DISTINCT employee_id FROM employees;
```

---

### ORDER BY

```sql
SELECT * FROM employees
ORDER BY full_name ASC;
```

---

### LIMIT & OFFSET

```sql
SELECT * FROM employees
LIMIT 2 OFFSET 1;
```

---

## Step 8️⃣ Aggregate Functions

```sql
SELECT COUNT(*) FROM employees;
```

```sql
SELECT MAX(employee_id) FROM employees;
```

---

## Step 9️⃣ GROUP BY (Basic)

```sql
SELECT employee_id, COUNT(*)
FROM employees
GROUP BY employee_id;
```

---

## Step 🔟 Transaction (Basic)

```sql
BEGIN;

UPDATE employees
SET full_name = 'JOHN'
WHERE employee_id = 4560;

COMMIT;
```

❌ Error হলে:

```sql
ROLLBACK;
```

---

## Complete Flow Summary

| Step | কাজ                           |
| ---- | ----------------------------- |
| 1    | Database তৈরি                 |
| 2    | Database connect              |
| 3    | Table তৈরি                    |
| 4    | Data insert                   |
| 5    | ALTER দিয়ে structure পরিবর্তন |
| 6    | SELECT দিয়ে data দেখা         |
| 7    | Aggregate / Group             |
| 8    | Transaction control           |

---





# SQL SELECT Basics — Query + Output + Explanation (Complete Notes)

---

## Sample Table (সব উদাহরণের জন্য)

ধরি আমাদের টেবিলটি এমন:

### students table

| id | name   | dept | age |
|----|--------|------|-----|
| 1  | Rahim  | CSE  | 22  |
| 2  | Karim  | EEE  | 20  |
| 3  | Salma  | CSE  | 24  |
| 4  | Anika  | BBA  | 21  |
| 5  | Arif   | EEE  | 23  |

---

## 18-3 SELECT Basics: Sorting & Aliases

### 🔹 ORDER BY (Sorting)

### Query

```sql
SELECT * FROM students
ORDER BY age ASC;
````

### Output

| id | name  | dept | age |
| -- | ----- | ---- | --- |
| 2  | Karim | EEE  | 20  |
| 4  | Anika | BBA  | 21  |
| 1  | Rahim | CSE  | 22  |
| 5  | Arif  | EEE  | 23  |
| 3  | Salma | CSE  | 24  |

### কেন এমন output?

* `ORDER BY age ASC` → বয়স অনুযায়ী **ছোট থেকে বড়**
* Default order হলো `ASC`

---

### 🔹 Aliases (AS)

### Query

```sql
SELECT name AS student_name, age AS student_age
FROM students;
```

### Output

| student_name | student_age |
| ------------ | ----------- |
| Rahim        | 22          |
| Karim        | 20          |
| Salma        | 24          |
| Anika        | 21          |
| Arif         | 23          |

### কেন এমন output?

* `AS` শুধু **column নাম বদলায়**
* ডেটা বদলায় না
* Output readable করার জন্য ব্যবহার হয়

---

## 18-4 DISTINCT & WHERE Filtering

### 🔹 DISTINCT

### Query

```sql
SELECT DISTINCT dept
FROM students;
```

### Output

| dept |
| ---- |
| CSE  |
| EEE  |
| BBA  |

### কেন এমন output?

* `dept` কলামে duplicate ছিল
* DISTINCT শুধু **unique value** দেখিয়েছে

---

### 🔹 WHERE Filtering

### Query

```sql
SELECT * FROM students
WHERE dept = 'CSE';
```

### Output

| id | name  | dept | age |
| -- | ----- | ---- | --- |
| 1  | Rahim | CSE  | 22  |
| 3  | Salma | CSE  | 24  |

### কেন এমন output?

* WHERE condition শুধু `dept = 'CSE'` match করা row দেখায়
* অন্য dept বাদ পড়ে

---

## 18-5 Filtering with AND & OR

### 🔹 AND

### Query

```sql
SELECT * FROM students
WHERE dept = 'CSE' AND age > 22;
```

### Output

| id | name  | dept | age |
| -- | ----- | ---- | --- |
| 3  | Salma | CSE  | 24  |

### কেন এমন output?

* `dept = 'CSE'` ✔
* `age > 22` ✔
* দুইটা শর্তই true হতে হবে

---

### 🔹 OR

### Query

```sql
SELECT * FROM students
WHERE dept = 'CSE' OR dept = 'EEE';
```

### Output

| id | name  | dept | age |
| -- | ----- | ---- | --- |
| 1  | Rahim | CSE  | 22  |
| 2  | Karim | EEE  | 20  |
| 3  | Salma | CSE  | 24  |
| 5  | Arif  | EEE  | 23  |

### কেন এমন output?

* যেকোনো একটাও true হলেই row select হয়
* BBA বাদ পড়ে

---

## 18-6 Comparison, BETWEEN & IN

### 🔹 Comparison Operator

### Query

```sql
SELECT * FROM students
WHERE age >= 23;
```

### Output

| id | name  | age |
| -- | ----- | --- |
| 3  | Salma | 24  |
| 5  | Arif  | 23  |

### কেন?

* `>= 23` condition match করছে শুধু এই দুইজন

---

### 🔹 BETWEEN

### Query

```sql
SELECT * FROM students
WHERE age BETWEEN 21 AND 23;
```

### Output

| id | name  | age |
| -- | ----- | --- |
| 1  | Rahim | 22  |
| 4  | Anika | 21  |
| 5  | Arif  | 23  |

### কেন?

* BETWEEN **inclusive**
* 21 এবং 23 দুইটাই ধরা হয়

---

### 🔹 IN

### Query

```sql
SELECT * FROM students
WHERE dept IN ('CSE', 'EEE');
```

### Output

| id | name  | dept |
| -- | ----- | ---- |
| 1  | Rahim | CSE  |
| 2  | Karim | EEE  |
| 3  | Salma | CSE  |
| 5  | Arif  | EEE  |

### কেন?

* IN মানে multiple OR
* Cleaner & readable

---

## 18-7 LIKE vs ILIKE

### 🔹 LIKE (Case-sensitive)

### Query

```sql
SELECT * FROM students
WHERE name LIKE 'A%';
```

### Output

| id | name  |
| -- | ----- |
| 4  | Anika |
| 5  | Arif  |

### কেন?

* `A%` → A দিয়ে শুরু
* `%` মানে যেকোনো character

---

### 🔹 ILIKE (PostgreSQL)

### Query

```sql
SELECT * FROM students
WHERE name ILIKE 'a%';
```

### Output

| id | name  |
| -- | ----- |
| 4  | Anika |
| 5  | Arif  |

### কেন?

* Case-insensitive
* `a%` ও `A%` একইভাবে কাজ করে

---

## 18-8 NOT & Scalar Functions

### 🔹 NOT

### Query

```sql
SELECT * FROM students
WHERE NOT dept = 'CSE';
```

### Output

| name  | dept |
| ----- | ---- |
| Karim | EEE  |
| Anika | BBA  |
| Arif  | EEE  |

### কেন?

* CSE বাদ দিয়ে বাকিগুলো দেখায়

---

### 🔹 Scalar Function (UPPER)

### Query

```sql
SELECT UPPER(name) FROM students;
```

### Output

| upper |
| ----- |
| RAHIM |
| KARIM |
| SALMA |
| ANIKA |
| ARIF  |

### কেন?

* Scalar function row-by-row কাজ করে

---

## 18-9 Aggregate Functions Explained

### 🔹 COUNT

```sql
SELECT COUNT(*) FROM students;
```

**Output:** `5`

👉 মোট row সংখ্যা

---

### 🔹 AVG

```sql
SELECT AVG(age) FROM students;
```

**Output:** `22`

👉 গড় বয়স

---


