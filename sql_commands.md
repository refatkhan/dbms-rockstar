
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


