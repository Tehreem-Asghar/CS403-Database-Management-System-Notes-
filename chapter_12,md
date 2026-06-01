# CS403 Database Management System
# Lecture 12 – Examination System Case Study (DFD, CRM & ER Diagram)

---

# Introduction

Is lecture mein hum ek Educational Institute ke Examination System ka complete analysis karte hain aur dekhte hain ke:

- DFD (Data Flow Diagram) kaise banti hai
- CRM (Cross Reference Matrix) kaise use hoti hai
- ER Diagram ke liye entities kaise identify ki jati hain
- Student Registration se lekar CGPA Calculation tak data kaise flow karta hai

Yeh lecture practical case study par based hai.

---

# Examination System Overview

System semester basis par kaam karta hai.

## System ke Main Features

- Students programs mein enroll hote hain.
- Programs multiple courses par mabni hote hain.
- Har semester courses offer kiye jate hain.
- Students courses register karte hain.
- Teacher classes conduct karta hai.
- Teacher quizzes, assignments aur exams leta hai.
- Result calculate hota hai.
- GPA aur CGPA calculate hota hai.
- Students ko transcript aur result card provide kiya jata hai.

---

# Real Life Example

Suppose:

Student Name: Ali

Program: BS Computer Science

Semester 3 mein following courses offer hue:

- Database Systems
- Data Structures
- Operating Systems

Ali ne pehle semester mein Programming Fundamentals fail kar diya tha.

Aur Programming Fundamentals Data Structures ki prerequisite hai.

Result:

✅ Ali Database Systems register kar sakta hai.

❌ Ali Data Structures register nahi kar sakta.

---

# Main Outputs Required

System se different users ko different reports milti hain.

## Students ke Liye

- Transcript
- Semester Result Card
- Subject Result

## Teachers ke Liye

- Attendance Sheet
- Class List
- Subject Result

## Controller Office ke Liye

- Subject Result
- Class Result
- Overall Semester Result

---

# Main Entities in System

System mein initially following entities nazar aati hain:

1. Student
2. Teacher
3. Controller
4. Course
5. Program
6. Registration
7. Result
8. Semester

---

# Context Diagram

Context Diagram sab se high level DFD hoti hai.

Yeh sirf external entities aur system ke interaction ko show karti hai.

## External Entities

### Registration System

Student ki registration verify karta hai.

### Teacher

Marks aur attendance submit karta hai.

### Controller

Reports receive karta hai.

### Student

Result aur transcript receive karta hai.

---

# Level 0 DFD

System ko 3 major modules mein divide kiya gaya.

## 1. Subject Registration

Student courses register karta hai.

## 2. Result Submission

Teacher marks submit karta hai.

## 3. Result Calculation

System GPA aur CGPA calculate karta hai.

---

# Module 1: Subject Registration

Yeh registration process ko handle karta hai.

---

## Process 1.0 - Registration Validation

Student registration form submit karta hai.

System check karta hai:

- Registration Number
- Student Information
- Semester Information
- Course Selection

Agar information valid ho:

✅ Next process mein bhej di jati hai.

Agar invalid ho:

❌ Registration reject kar di jati hai.

---

## Real Example

Student:

Ali

Selected Courses:

- Database Systems
- Operating Systems

System check karega:

- Student registered hai?
- Semester active hai?
- Required information complete hai?

Agar sab sahi hai:

Registration accept.

---

# Process 2.0 - Prerequisite Checking

Ab system check karega:

Kya student ne required prerequisite courses pass kiye hain?

---

## Real Example

Course:

Data Structures

Prerequisite:

Programming Fundamentals

Agar student ne Programming Fundamentals pass nahi kiya:

❌ Data Structures register nahi kar sakta.

Agar pass kiya hua hai:

✅ Registration allow hogi.

---

# Registration Database

Verification ke baad student ki registration save ho jati hai.

### Stored Data

- Student ID
- Semester
- Registered Courses

Yeh data future processes use karte hain.

---

# Module 2: Result Submission

Teacher result submit karta hai.

External Entity:

Teacher

---

# Process 3.0 - Result Collection

Teacher alag alag components ke marks submit karta hai.

---

## Result Components

### Assignments

Example:

18/20

---

### Quizzes

Example:

8/10

---

### Sessionals

Example:

14/15

---

### Midterm

Example:

20/25

---

### Final Exam

Example:

35/50

---

# Real Example

Student: Ali

| Component | Marks |
|------------|---------|
| Assignment | 18 |
| Quiz | 8 |
| Sessional | 14 |
| Midterm | 20 |
| Final | 35 |

Total:

95 Marks

---

# Process 4.0 - Calculate GP

System marks ko Grade aur GP mein convert karta hai.

---

## Example Grading Table

| Marks | Grade | GP |
|---------|---------|---------|
| 85-100 | A | 4.0 |
| 75-84 | B | 3.0 |
| 65-74 | C | 2.0 |
| 50-64 | D | 1.0 |
| Below 50 | F | 0 |

---

## Example

Ali = 95 Marks

Grade = A

GP = 4.0

---

# Process 5.0 - Update Result

Calculated result database mein save kar diya jata hai.

Updated Data:

- Marks
- Grade
- GP

---

# Module 3: GPA Calculation

Ab tamam subjects ke GP use karke GPA calculate hota hai.

---

# GPA (Grade Point Average)

Formula:

GPA = Sum of Subject GPs / Total Subjects

---

## Example

| Subject | GP |
|----------|------|
| DBMS | 4.0 |
| DSA | 3.5 |
| OS | 3.0 |

GPA =

(4.0 + 3.5 + 3.0) / 3

= 3.5

---

# Process 7.0 - CGPA Calculation

CGPA calculate karne ke liye previous semesters ke GPA bhi use kiye jate hain.

---

## Example

| Semester | GPA |
|------------|---------|
| 1 | 3.20 |
| 2 | 3.60 |
| 3 | 3.80 |

CGPA =

(3.20 + 3.60 + 3.80) / 3

= 3.53

---

# Detailed DFD

Level 0 DFD ko aur detail mein expand karne ko Detailed DFD kehte hain.

---

## Example

Registration Module

↓

Validate Form

↓

Check Prerequisites

↓

Approve Registration

↓

Store Data

---

# Cross Reference Matrix (CRM)

CRM batati hai:

Kaunsa attribute kis report mein use hoga.

---

# CRM Structure

Rows:

Attributes

Columns:

Reports

---

## Example CRM

| Attribute | Transcript | Result Card | Attendance | Class Result |
|------------|------------|------------|------------|------------|
| Reg No | ✔ | ✔ | ✔ | ✔ |
| Student Name | ✔ | ✔ | ✔ | ✔ |
| Course Name | ✔ | ✔ | ❌ | ✔ |
| GPA | ✔ | ✔ | ❌ | ❌ |
| CGPA | ✔ | ✔ | ❌ | ❌ |

---

# CRM ka Purpose

CRM se hume pata chalta hai:

- Kaunsa data kis report mein chahiye
- Kaunsi entities exist karti hain
- Kaunse attributes kis entity ke hain

---

# CRM se Entity Identification

Transcript ko dekhein.

Is mein:

- Reg No
- Student Name
- Father Name

Student ki information hai.

To yeh Student Entity mein jayenge.

---

## Academic Information

Transcript mein:

- Course Name
- Grade
- GPA
- CGPA

Academic information hai.

Yeh Course aur Result Entities mein jayegi.

---

# ER Diagram Creation

ER Diagram banane ka pehla step:

Entities identify karna.

---

## Identified Entities

### Student

Attributes:

- Reg_No
- Student_Name
- Father_Name
- CGPA

---

### Course

Attributes:

- Course_ID
- Course_Name
- Credit_Hours

---

### Teacher

Attributes:

- Teacher_ID
- Teacher_Name

---

### Program

Attributes:

- Program_ID
- Program_Name

---

### Registration

Attributes:

- Registration_ID
- Semester
- Registration_Date

---

### Result

Attributes:

- Marks
- Grade
- GP

---

### Semester

Attributes:

- Semester_ID
- Semester_Name

---

# Controller ER Diagram Mein Kyun Nahi Aya?

Controller DFD mein external entity tha.

Lekin ER Diagram mein include nahi kiya gaya.

Reason:

Sirf ek controller hota hai.

ER Diagram normally un cheezon ke liye banti hai jin ki multiple instances hoti hain.

---

## Example

Student Entity

- Student 1
- Student 2
- Student 3
- Student 100

Multiple instances available.

Controller:

- Sirf 1 Controller

Isliye entity nahi banayi gayi.

---

# Result Entity Special Case

Result ko directly entity banana mushkil hota hai.

Kyun ke:

- Assignment Result
- Quiz Result
- Midterm Result
- Final Result

Sab different results hain.

Isliye detailed analysis ke baad proper structure design ki jati hai.

---

# Important Exam Points

## DFD

Data flow ko show karti hai.

---

## CRM

Reports aur attributes ka relation show karti hai.

---

## ER Diagram

Database structure ko represent karti hai.

---

## Registration Module

Student registration aur prerequisite checking karta hai.

---

## Result Submission Module

Teacher marks submit karta hai.

---

## Result Calculation Module

GP, GPA aur CGPA calculate karta hai.

---

# One Line Revision

- Context Diagram = Complete system ka high level view.
- DFD = Data flow show karti hai.
- CRM = Attribute aur reports ka relation show karti hai.
- Registration Module = Course registration handle karta hai.
- Result Submission = Teacher marks submit karta hai.
- GP = Subject level performance.
- GPA = Semester level average.
- CGPA = Overall academic performance.
- ER Diagram = Database structure ka graphical model.
