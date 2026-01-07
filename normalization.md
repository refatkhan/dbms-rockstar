# Normalization, Functional Dependency & ACID Properties (DBMS)

---

## 🔹 Normalization (ডেটাবেস নরমালাইজেশন)

Normalization হলো এমন একটি প্রক্রিয়া যার মাধ্যমে ডেটাবেসকে  
**সুশৃঙ্খল, redundancy-free এবং anomaly-free** করা হয়।

---

## Normalization কেন দরকার?

| কারণ | ব্যাখ্যা |
|----|---------|
| Redundancy কমায় | একই ডেটা বারবার রাখা লাগে না |
| Anomaly দূর করে | Insert, Update, Delete সমস্যা কমে |
| Data Integrity | ডেটা সঠিক ও consistent থাকে |
| Maintenance সহজ | Database manage করা সহজ হয় |

---

## 🔸 1NF (First Normal Form)

### 1NF এর নিয়ম

| শর্ত | ব্যাখ্যা |
|----|---------|
| Atomic Value | প্রতিটি কলামে single value থাকবে |
| Repeating Group না | এক কলামে একাধিক মান থাকবে না |

---

### ❌ 1NF ভাঙা টেবিল

| StudentID | Name  | Courses        |
|----------|-------|----------------|
| 101 | Rahim | DBMS, OOP |

---

### ✅ 1NF অনুসারে টেবিল

| StudentID | Name  | Course |
|----------|-------|--------|
| 101 | Rahim | DBMS |
| 101 | Rahim | OOP  |

---

### SQL Example (1NF)

```sql
CREATE TABLE StudentCourse (
    StudentID INT,
    StudentName VARCHAR(50),
    Course VARCHAR(50)
);

```
---

## 🔸 2NF (Second Normal Form)

---

## 2NF এর নিয়ম

| শর্ত | ব্যাখ্যা |
|-----|---------|
| 1NF হতে হবে | Table অবশ্যই 1NF এ থাকতে হবে |
| Partial Dependency না | Non-key attribute পুরো Primary Key-এর উপর নির্ভর করবে |

📌 **Partial Dependency** তখন হয় যখন  
Composite Primary Key–এর **একটি অংশের উপর** কোনো Non-key attribute নির্ভর করে।

---

## ❌ 2NF ভাঙা টেবিল

| StudentID | CourseID | StudentName | CourseName |
|-----------|----------|-------------|------------|

**Primary Key:** `(StudentID, CourseID)`

➡️ এখানে  
`StudentName` শুধু `StudentID`-এর উপর নির্ভর করছে ❌  
➡️ তাই এটি **2NF ভঙ্গ করছে**

---

## ✅ 2NF অনুসারে টেবিল

### Student Table

| StudentID | StudentName |
|-----------|-------------|

---

### Course Table

| CourseID | CourseName |
|----------|------------|

---

### Enrollment Table

| StudentID | CourseID |
|-----------|----------|

---

## SQL Example (2NF)

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50)
);

CREATE TABLE Course (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(50)
);

CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID)
);

```

---

❌ এটি একটি **Transitive Dependency**, তাই টেবিলটি **3NF ভঙ্গ করছে**

---

## ✅ 3NF অনুসারে টেবিল

### Student Table

| StudentID | Name | DeptID |
|-----------|------|--------|

---

### Department Table

| DeptID | DeptName |
|--------|----------|

---

## SQL Example (3NF)

```sql
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

---

## 🔹 Functional Dependency (FD)

---

## Functional Dependency কী?

যখন একটি Attribute অন্য একটি Attribute-এর মান নির্ধারণ করে,  
তখন তাকে **Functional Dependency (FD)** বলা হয়।

---

## লেখার নিয়ম

A → B


মানে:  
👉 **A জানা থাকলে B নির্দিষ্টভাবে জানা যাবে**

---

## Standard Example Table

| StudentID | StudentName | DeptID |
|-----------|-------------|--------|

➡️ `StudentID → StudentName`  
➡️ `StudentID → DeptID`

---

## FD এর প্রকারভেদ (Table সহ)

---

### 1️⃣ Full Functional Dependency

| Dependency | ব্যাখ্যা |
|------------|---------|
| (StudentID, CourseID) → Grade | পুরো Primary Key-এর উপর নির্ভর |

---

### 2️⃣ Partial Dependency

| Dependency | সমস্যা |
|------------|-------|
| (StudentID, CourseID) → StudentName | PK-এর একটি অংশের উপর নির্ভর ❌ |

---

### 3️⃣ Transitive Dependency

| Dependency Chain | সমস্যা |
|------------------|-------|
| StudentID → DeptID → DeptName | Non-key → Non-key নির্ভরতা ❌ |

---

## সংক্ষেপে (FD)
> **Functional Dependency ডেটাবেসে Attribute গুলোর পারস্পরিক সম্পর্ক বোঝাতে সাহায্য করে  
এবং Normalization-এর ভিত্তি তৈরি করে।**

---

## 🔹 ACID Properties

ACID Properties নিশ্চিত করে যে Database Transaction  
**Safe, Reliable এবং Consistent** হবে।

---

## ACID Properties (Table Format)

| Property | অর্থ | Real-Life Example |
|----------|-----|------------------|
| Atomicity | সব না হলে কিছুই না | টাকা কাটা হলে জমাও হবেই |
| Consistency | Valid state বজায় | Balance কখনো negative হবে না |
| Isolation | Transaction আলাদা | দুইজন একসাথে টাকা তুললেও সমস্যা না |
| Durability | Commit স্থায়ী | System crash হলেও ডেটা থাকবে |

---

## ACID – SQL Context Example

```sql
BEGIN TRANSACTION;

UPDATE Account 
SET Balance = Balance - 500 
WHERE AccNo = 101;

UPDATE Account 
SET Balance = Balance + 500 
WHERE AccNo = 102;

COMMIT;

➡️ Commit হলে টাকা transfer স্থায়ী
➡️ Error হলে ROLLBACK হবে

```
---

## Final Summary

| Topic                 | মূল উদ্দেশ্য             |
| --------------------- | ------------------------ |
| Normalization         | Redundancy ও Anomaly দূর |
| Functional Dependency | Attribute সম্পর্ক বোঝা   |
| ACID Properties       | Transaction নিরাপদ করা   |

---