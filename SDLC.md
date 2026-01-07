## SDLC অনুযায়ী Database Design Process (ধাপে ধাপে)

বাস্তব জীবনে কোনো প্রজেক্ট এলে আমরা সরাসরি টেবিল বানানো শুরু করি না।  
Database Design সবসময় **SDLC (Software Development Life Cycle)** অনুসরণ করে করা হয়।

নিচে একটি **বাস্তব প্রজেক্ট উদাহরণ (University Management System)** ধরে  
ধাপে ধাপে Database Design Process ব্যাখ্যা করা হলো।

---

## Step 1: Requirement Analysis (প্রয়োজন নির্ধারণ)

### এই ধাপে কী করি?
- ক্লায়েন্ট / স্টেকহোল্ডারের সাথে কথা বলি  
- তারা কী চায়, কী সমস্যা সমাধান করতে চায় তা বুঝি  
- ডেটা কী কী থাকবে তা লিস্ট করি  

### বাস্তব উদাহরণ
University Project এ ক্লায়েন্ট বললো:
- Student তথ্য রাখতে হবে  
- Course তথ্য রাখতে হবে  
- Teacher তথ্য রাখতে হবে  
- Student কোন Course নিয়েছে সেটা ট্র্যাক করতে হবে  

### Output
- Requirement Document  
- Data List (Student, Course, Teacher, Enrollment)

---

## Step 2: Feasibility Study (সম্ভবতা যাচাই)

### এই ধাপে কী করি?
- প্রজেক্ট করা বাস্তবসম্মত কিনা দেখি  
- সময়, খরচ ও প্রযুক্তি যাচাই করি  

### প্রশ্ন করি
- কত ডেটা হবে?  
- Concurrent user কতজন?  
- MySQL যথেষ্ট নাকি PostgreSQL লাগবে?  

### Output
- DBMS নির্বাচন (যেমন: MySQL)  
- High-level সিদ্ধান্ত  

---

## Step 3: Conceptual Database Design (ER Diagram)

### এই ধাপে কী করি?
- Entity চিহ্নিত করি  
- Attribute নির্ধারণ করি  
- Relationship তৈরি করি  

### বাস্তব উদাহরণ
**Entities**
- Student  
- Course  
- Teacher  

**Relationships**
- Student enrolls Course  
- Teacher teaches Course  

### Output
- ER Diagram  
- Primary Key ও Foreign Key ধারণা  

---

## Step 4: Logical Database Design (Schema Design)

### বাস্তব উদাহরণ
Student(StudentID, Name, Email, Dept)
Course(CourseID, CourseName, Credit)
Enrollment(StudentID, CourseID)


---

## Step 5: Normalization (ডেটা অপটিমাইজেশন)

আগে:
StudentID, Name, CourseName, TeacherName


Normalization করার পরে:
Student(StudentID, Name)
Course(CourseID, CourseName)
Teacher(TeacherID, Name)


---

## Step 6: Physical Database Design

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Email VARCHAR(100)
);
Step 7: Database Implementation
সব টেবিল তৈরি

Constraint সেট

Sample data insert

Step 8: Testing & Validation
    1.Duplicate PK check
    2.FK violation check

Step 9: Deployment
    1.Production server
    2.App connection

Step 10: Maintenance & Optimization
    1.Backup
    2.Performance tuning