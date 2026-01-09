# SQL (Structured Query Language) — Complete Notes

---

## SQL কী?

**SQL (Structured Query Language)** হলো সেই ভাষা  
যার মাধ্যমে আমরা **Database-এর সাথে কথা বলি**।

📌 সহজভাবে:
> **SQL হলো Database-এর ভাষা**

---

## SQL-এর ইতিহাস (সংক্ষেপে)

- ১৯৭০-এর দশকে **IBM** এ তৈরি  
- ১৯৮৬ সালে **Standard** হিসেবে স্বীকৃত  
- আজও সব Modern Database-এর Backbone  

📌 MySQL, PostgreSQL, Oracle, SQL Server — সবখানেই SQL ব্যবহৃত হয় :contentReference[oaicite:1]{index=1}

---

## SQL কেন Declarative Language?

### Declarative মানে কী?
SQL হলো **Declarative Language**, অর্থাৎ:

> তুমি Database-কে বলো **কি চাও**,  
> কিন্তু **কিভাবে করবে সেটা Database নিজেই ঠিক করে**।

### উদাহরণ
```sql
SELECT * FROM students WHERE dept = 'CSE';
```

---

## Categories of SQL Commands

SQL Command গুলোকে সাধারণত **৫ ভাগে** ভাগ করা হয়।

---

## 1️⃣ DDL — Data Definition Language

👉 **Database structure তৈরি ও পরিবর্তনের জন্য** ব্যবহৃত হয়।

### Commands

| Command | কাজ |
|--------|-----|
| CREATE | Table / Database তৈরি |
| DROP | সম্পূর্ণ delete |
| ALTER | Structure পরিবর্তন |
| TRUNCATE | Data delete (structure থাকবে) |

### উদাহরণ
```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(50)
);
```

---

## 2️⃣ DQL — Data Query Language

👉 **Database থেকে ডেটা বের করার জন্য** ব্যবহৃত হয়।

### Command

| Command | কাজ |
|--------|-----|
| SELECT | Data retrieve |

### উদাহরণ
```sql
SELECT name, age 
FROM students;
````

 **ব্যবহার হবে যখন:**

* Data দেখাতে হবে
* Report তৈরি করতে হবে
* Filter / Search করতে হবে

---

## 3️⃣ DML — Data Manipulation Language

 **Table-এর ভিতরের ডেটা পরিবর্তনের জন্য** ব্যবহৃত হয়।

### Commands

| Command | কাজ                    |
| ------- | ---------------------- |
| INSERT  | নতুন data যোগ          |
| UPDATE  | বিদ্যমান data পরিবর্তন |
| DELETE  | data মুছে ফেলা         |

### উদাহরণ

#### INSERT

```sql
INSERT INTO students (name, age)
VALUES ('Rahim', 22);
```

#### UPDATE

```sql
UPDATE students
SET age = 23
WHERE name = 'Rahim';
```

#### DELETE

```sql
DELETE FROM students
WHERE name = 'Rahim';
```

 **ব্যবহার হবে যখন:**

* নতুন record যোগ করতে হবে
* ভুল data সংশোধন করতে হবে
* অপ্রয়োজনীয় data মুছতে হবে

---

## 4️⃣ DCL — Data Control Language

👉 **Database security ও user permission নিয়ন্ত্রণের জন্য** ব্যবহৃত হয়।

### Commands

| Command | কাজ               |
| ------- | ----------------- |
| GRANT   | Permission দেওয়া |
| REVOKE  | Permission বাতিল  |

### উদাহরণ

#### GRANT

```sql
GRANT SELECT, INSERT
ON students
TO user1;
```

#### REVOKE

```sql
REVOKE INSERT
ON students
FROM user1;
```

 **ব্যবহার হবে যখন:**

* Multi-user system
* কে কোন data access করবে নিয়ন্ত্রণ দরকার

---

## 5️⃣ TCL — Transaction Control Language

👉 **Transaction manage করার জন্য** ব্যবহৃত হয়।

### Commands

| Command  | কাজ                |
| -------- | ------------------ |
| COMMIT   | Change স্থায়ী করা |
| ROLLBACK | Change বাতিল করা   |

### উদাহরণ

```sql
BEGIN;

UPDATE account
SET balance = balance - 500
WHERE acc_no = 101;

UPDATE account
SET balance = balance + 500
WHERE acc_no = 102;

COMMIT;
```

### যদি কোনো error হয়:

```sql
ROLLBACK;
```

 **ব্যবহার হবে যখন:**

* Banking system
* Payment / Transfer
* Critical data operation

---

## সংক্ষেপে তুলনা

| Category | কী নিয়ন্ত্রণ করে         |
| -------- | ------------------------- |
| DQL      | Data দেখা                 |
| DML      | Data পরিবর্তন             |
| DCL      | Security & Permission     |
| TCL      | Transaction & Consistency |

> **একটি সঠিক Database System এই চারটি SQL Category ছাড়া অসম্পূর্ণ।**

