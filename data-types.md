
## SQL Data Types (Why + When + Example)

SQL Data Type নির্ধারণ করে  
👉 **কোন ধরনের ডেটা রাখা যাবে**  
👉 **কত জায়গা (memory) লাগবে**  
👉 **ডেটা কতটা সঠিক ও efficient হবে**

📌 সঠিক Data Type নির্বাচন করলে:
- Data accuracy বাড়ে  
- Memory waste কমে  
- Query performance ভালো হয়  

---

## 🔹 Boolean Data Type

### কেন ব্যবহার করি?
Yes / No, True / False ধরনের মান সংরক্ষণের জন্য।

### কখন ব্যবহার করবো?
- Active / Inactive
- Approved / Not Approved

| Data Type | মান |
|----------|----|
| BOOLEAN | TRUE, FALSE, NULL |

### SQL Example
```sql
is_active BOOLEAN
````

---

## 🔹 Numeric Data Types

### Integer Types (Whole Number)

| Data Type | Size    | কখন ব্যবহার করবো | কেন            |
| --------- | ------- | ---------------- | -------------- |
| SMALLINT  | 2 bytes | বয়স, quantity    | ছোট সংখ্যা     |
| INTEGER   | 4 bytes | ID, count        | Default choice |
| BIGINT    | 8 bytes | বড় counter, logs | Huge range     |

```sql
age SMALLINT,
employee_id INTEGER
```

---

### Decimal / Floating Types

| Data Type         | কখন ব্যবহার করবো  | কেন                 |
| ----------------- | ----------------- | ------------------- |
| REAL / DOUBLE     | Approximate value | Sensor, measurement |
| DECIMAL / NUMERIC | Exact value       | টাকা, balance       |

📌 **Money-এর জন্য সবসময় DECIMAL ব্যবহার করবে**
কারণ Floating type–এ rounding error হয়।

```sql
salary DECIMAL(10,2)
```

---

### SERIAL (Auto Increment)

| Data Type | কখন ব্যবহার করবো     |
| --------- | -------------------- |
| SERIAL    | Primary Key, Auto ID |

```sql
id SERIAL PRIMARY KEY
```

---

## 🔹 Character (Text) Data Types

| Data Type  | কখন ব্যবহার করবো | কেন          |
| ---------- | ---------------- | ------------ |
| CHAR(n)    | Fixed length     | Country code |
| VARCHAR(n) | Limited text     | Name, Email  |
| TEXT       | Long text        | Description  |

```sql
name VARCHAR(50),
description TEXT
```

---

## 🔹 Date & Time Data Types

| Data Type   | কখন ব্যবহার করবো |
| ----------- | ---------------- |
| DATE        | জন্ম তারিখ       |
| TIME        | নির্দিষ্ট সময়    |
| TIMESTAMP   | Date + Time      |
| TIMESTAMPTZ | Timezone সহ      |

```sql
dob DATE,
created_at TIMESTAMPTZ
```

---

## 🔹 UUID Data Type

### কেন ব্যবহার করি?

Globally unique ID দরকার হলে।

### কখন ব্যবহার করবো?

* Distributed system
* Microservices

```sql
id UUID
```

---

## 🔹 Constraints (With Full Example)

Constraint ব্যবহার করা হয়
👉 **ভুল ডেটা ঢোকা আটকাতে**
👉 **Data integrity বজায় রাখতে**

---

## Types of Constraints

| Constraint  | কাজ                |
| ----------- | ------------------ |
| NOT NULL    | মান দিতেই হবে      |
| UNIQUE      | Duplicate চলবে না  |
| PRIMARY KEY | Unique + Not Null  |
| FOREIGN KEY | Table relation     |
| DEFAULT     | Value না দিলে auto |
| CHECK       | Condition enforce  |

---

## 🔹 Full Constraint Example (One Table)

```sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,        -- PRIMARY KEY
    full_name VARCHAR(100) NOT NULL,       -- NOT NULL
    email VARCHAR(100) UNIQUE,              -- UNIQUE
    age INT CHECK (age >= 18),              -- CHECK
    status VARCHAR(20) DEFAULT 'active'     -- DEFAULT
);
```

---

## 🔹 Foreign Key Example

```sql
CREATE TABLE courses (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR(50)
);

CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

📌 এখানে:

* `student_id` → students table-এর Primary Key
* `course_id` → courses table-এর Primary Key

---

## Constraint কেন গুরুত্বপূর্ণ?

| সমস্যা      | Constraint ছাড়া | Constraint সহ |
| ----------- | ---------------- | ------------- |
| NULL value  | ঢুকে যাবে ❌      | আটকাবে ✅      |
| Duplicate   | সম্ভব ❌          | অসম্ভব ✅      |
| Invalid age | ঢুকে যাবে ❌      | আটকাবে ✅      |

---

## Final Summary

| Topic          | মূল উদ্দেশ্য           |
| -------------- | ---------------------- |
| SQL Data Types | Accuracy + Performance |
| Constraints    | Data Integrity         |

> **ভালো Database Design = সঠিক Data Type + সঠিক Constraint**


