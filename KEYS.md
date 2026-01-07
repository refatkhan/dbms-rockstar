
## Keys in DBMS (ডিবিএমএস-এ কী)

DBMS–এ **Key** হলো এমন একটি অ্যাট্রিবিউট বা অ্যাট্রিবিউটের সমষ্টি,  
যার মাধ্যমে একটি টেবিলের প্রতিটি রেকর্ডকে **ইউনিকভাবে শনাক্ত** করা যায়।

---

### 1. Super Key
**Super Key** হলো এমন একটি কী, যা একটি টেবিলের প্রতিটি রেকর্ডকে আলাদাভাবে শনাক্ত করতে পারে।

#### বৈশিষ্ট্য
- এক বা একাধিক অ্যাট্রিবিউট নিয়ে গঠিত  
- অতিরিক্ত অ্যাট্রিবিউট থাকতে পারে  

#### উদাহরণ (Conceptual)
```

StudentID
StudentID + Email

````

#### SQL উদাহরণ
```sql
SELECT * FROM Students WHERE StudentID = 101 AND Email = 'abc@gmail.com';
````

---

### 2. Candidate Key

**Candidate Key** হলো Super Key–এর মধ্যে থেকে সর্বনিম্ন (minimal) কী।

#### বৈশিষ্ট্য

* কোনো অতিরিক্ত অ্যাট্রিবিউট থাকে না
* অবশ্যই ইউনিক

#### উদাহরণ

```
StudentID
Email
```

#### SQL উদাহরণ

```sql
CREATE TABLE Students (
    StudentID INT,
    Email VARCHAR(100),
    Name VARCHAR(50),
    UNIQUE (StudentID),
    UNIQUE (Email)
);
```

---

### 3. Primary Key

**Primary Key** হলো Candidate Key–এর মধ্য থেকে নির্বাচিত প্রধান কী।

#### বৈশিষ্ট্য

* NULL হতে পারবে না
* Duplicate হবে না
* একটি টেবিলে একটিমাত্র Primary Key

#### উদাহরণ

```
StudentID
```

#### SQL উদাহরণ

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Dept VARCHAR(20)
);
```

---

### 4. Alternate Key

Primary Key ছাড়া বাকি Candidate Key গুলোকে **Alternate Key** বলা হয়।

#### উদাহরণ

```
Candidate Keys: StudentID, Email
Primary Key: StudentID
Alternate Key: Email
```

#### SQL উদাহরণ

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE
);
```

---

### 5. Foreign Key

**Foreign Key** একটি টেবিলের কলাম, যা অন্য টেবিলের Primary Key–কে রেফার করে।

#### কাজ

* টেবিলের মধ্যে সম্পর্ক তৈরি করে
* Referential Integrity বজায় রাখে

#### উদাহরণ

```
Enrollment.StudentID → Students.StudentID
```

#### SQL উদাহরণ

```sql
CREATE TABLE Enrollment (
    EnrollID INT PRIMARY KEY,
    StudentID INT,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);
```

---

### 6. Composite Key

যখন দুই বা ততোধিক অ্যাট্রিবিউট একসাথে মিলে একটি কী তৈরি করে।

#### উদাহরণ

```
(StudentID + CourseID)
```

#### SQL উদাহরণ

```sql
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID)
);
```

---

### 7. Unique Key

**Unique Key** নিশ্চিত করে যে একটি কলামের মান ইউনিক হবে।

#### বৈশিষ্ট্য

* Duplicate মান গ্রহণ করে না
* NULL থাকতে পারে (DBMS ভেদে সীমিত)

#### SQL উদাহরণ

```sql
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    NID VARCHAR(20) UNIQUE
);
```

---

### 8. Surrogate Key

**Surrogate Key** হলো কৃত্রিমভাবে তৈরি করা কী, যার বাস্তব অর্থ নেই।

#### বৈশিষ্ট্য

* সাধারণত Auto Increment
* সিস্টেম দ্বারা নিয়ন্ত্রিত

#### SQL উদাহরণ

```sql
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    OrderDate DATE
);
```

---

### 9. Natural Key

**Natural Key** বাস্তব জীবনের অর্থপূর্ণ ডেটা থেকে তৈরি হয়।

#### উদাহরণ

```
Email
National ID
```

#### SQL উদাহরণ

```sql
CREATE TABLE Citizens (
    NID VARCHAR(20) PRIMARY KEY,
    Name VARCHAR(50)
);
```

---

### 10. Secondary Key

**Secondary Key** ব্যবহার করা হয় ডেটা সার্চ বা ফিল্টার করার জন্য।
এটি ইউনিক নাও হতে পারে।

#### উদাহরণ

```
Department
```

#### SQL উদাহরণ

```sql
SELECT * FROM Students WHERE Dept = 'CSE';
```

---

## সংক্ষেপে বললে

> **Keys ডেটার ইউনিকনেস, সম্পর্ক এবং ডেটা ইন্টেগ্রিটি নিশ্চিত করার মূল ভিত্তি।**

```


---

## Key গুলোর সংক্ষিপ্ত তুলনা

| Key Type        | ইউনিক | NULL | সংখ্যা |
|-----------------|------|------|--------|
| Super Key       | হ্যাঁ | না   | একাধিক |
| Candidate Key   | হ্যাঁ | না   | একাধিক |
| Primary Key     | হ্যাঁ | না   | একটিমাত্র |
| Alternate Key   | হ্যাঁ | না   | একাধিক |
| Foreign Key     | না   | হ্যাঁ | একাধিক |
| Composite Key   | হ্যাঁ | না   | একাধিক |
| Unique Key      | হ্যাঁ | হ্যাঁ | একাধিক |

---

