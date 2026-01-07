```md
# DBMS-এ Keys (চাবি) — সম্পূর্ণ নোটস

DBMS–এ **Key** হলো এমন একটি অ্যাট্রিবিউট বা অ্যাট্রিবিউটের সমষ্টি,  
যার মাধ্যমে টেবিলের প্রতিটি রেকর্ডকে **আলাদাভাবে শনাক্ত (identify)** করা যায়।

---

## 1. Super Key
**Super Key** হলো এমন একটি কী, যা টেবিলের প্রতিটি রেকর্ডকে ইউনিকভাবে শনাক্ত করতে পারে।

### বৈশিষ্ট্য
- এক বা একাধিক অ্যাট্রিবিউট নিয়ে গঠিত  
- অতিরিক্ত (unnecessary) অ্যাট্রিবিউট থাকতে পারে  

### উদাহরণ
```

StudentID
StudentID + Name
StudentID + Email

```

---

## 2. Candidate Key
**Candidate Key** হলো Super Key–এর মধ্যে থেকে **সর্বনিম্ন (minimal)** কী।

### বৈশিষ্ট্য
- কোনো অপ্রয়োজনীয় অ্যাট্রিবিউট থাকে না  
- প্রতিটি Candidate Key ইউনিক  

### উদাহরণ
```

StudentID
Email

```

---

## 3. Primary Key
**Primary Key** হলো Candidate Key–এর মধ্যে থেকে নির্বাচিত প্রধান কী।

### বৈশিষ্ট্য
- NULL হতে পারবে না  
- অবশ্যই ইউনিক হতে হবে  
- একটি টেবিলে একটিমাত্র Primary Key থাকে  

### উদাহরণ
```

StudentID (Primary Key)

```

---

## 4. Alternate Key
Primary Key ছাড়া বাকি Candidate Key গুলোকে **Alternate Key** বলা হয়।

### উদাহরণ
```

Candidate Keys: StudentID, Email
Primary Key: StudentID
Alternate Key: Email

```

---

## 5. Foreign Key
**Foreign Key** একটি টেবিলের কলাম, যা অন্য টেবিলের Primary Key–কে রেফার করে।

### কাজ
- টেবিলগুলোর মধ্যে সম্পর্ক (Relationship) তৈরি করে  
- Referential Integrity বজায় রাখে  

### উদাহরণ
```

Student(StudentID) → Enrollment(StudentID)

```

---

## 6. Composite Key
যখন দুই বা তার বেশি অ্যাট্রিবিউট একসাথে মিলে একটি কী গঠন করে, তখন তাকে **Composite Key** বলা হয়।

### উদাহরণ
```

(StudentID + CourseID)

```

---

## 7. Unique Key
**Unique Key** নিশ্চিত করে যে কলামের প্রতিটি মান আলাদা হবে।

### বৈশিষ্ট্য
- NULL থাকতে পারে (DBMS অনুযায়ী সীমিত)  
- একটি টেবিলে একাধিক Unique Key থাকতে পারে  

---

## 8. Surrogate Key
**Surrogate Key** হলো কৃত্রিমভাবে তৈরি করা কী।

### বৈশিষ্ট্য
- বাস্তব জীবনের কোনো অর্থ নেই  
- সাধারণত Auto Increment হয়  

### উদাহরণ
```

ID = 1, 2, 3, 4 ...

```

---

## 9. Natural Key
**Natural Key** হলো বাস্তব জীবনের অর্থপূর্ণ ও স্বাভাবিক কী।

### উদাহরণ
```

National ID
Email Address
Passport Number

```

---

## 10. Secondary Key
**Secondary Key** ব্যবহার করা হয় ডেটা **সার্চ বা ফিল্টার** করার জন্য,  
এটি ইউনিক নাও হতে পারে।

### উদাহরণ
```

Department
City

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

