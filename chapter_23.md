# 📘 Database Management System (CS403)
# Lecture 23 – Physical Record, Denormalization & Partitioning
---

# 🎯 Lecture Overview

Is lecture mein hum 2 important concepts parhenge.

1. Physical Record & Denormalization
2. Partitioning

Pichli lectures mein hum database ko **Normalize** kar rahe thay taake redundancy kam ho aur anomalies na aayen.

Lekin is lecture mein hum seekhenge ke kabhi kabhi **performance improve karne ke liye Normalization ko thora compromise bhi karna padta hai.**

Isi process ko **Denormalization** kehte hain.

Uske baad hum **Partitioning** seekhenge jisme ek bari table ko chhoti tables mein divide kiya jata hai.

---

# Revision (Normalization vs Denormalization)

Sab se pehle difference samajh lo.

| Normalization | Denormalization |
|---------------|-----------------|
| Tables ko divide karta hai | Tables ko merge karta hai |
| Redundancy kam hoti hai | Redundancy barh sakti hai |
| Data safe hota hai | Performance fast hoti hai |
| Joins zyada lagti hain | Joins kam lagti hain |
| Storage efficient | Storage thori zyada use hoti hai |

---

# Physical Database Design

Database Design ke do stages hotay hain.

## 1. Logical Database Design

Is stage mein sirf relationship aur structure banaya jata hai.

Hum sochte hain:

- Kon si tables hongi
- Primary Key kya hogi
- Foreign Key kya hogi

Example

```
Student
--------
StudentID
Name
DepartmentID
```

Ye sirf logical structure hai.

---

## 2. Physical Database Design

Is stage mein socha jata hai ke

- Data hard disk par kaise save hoga
- Records kis order mein honge
- Index kahan banega
- Tables merge karni hain ya nahi

Yahan performance sab se important hoti hai.

---

# Denormalization

## Definition

Denormalization ek technique hai jisme database ko intentionally less normalized banaya jata hai taake queries jaldi execute ho sakein.

Simple words mein

> **Tables ko merge karna taake joins kam ho jayein aur speed barh jaye.**

---

# Real Life Example

Socho ek School ka database hai.

## Student Table

| StudentID | Name |
|-----------|------|
| 1 | Ali |
| 2 | Ahmed |

---

## Department Table

| DepartmentID | Department |
|--------------|------------|
| 10 | CS |
| 20 | IT |

---

Student Table

| StudentID | Name | DepartmentID |
|-----------|------|--------------|
|1|Ali|10|
|2|Ahmed|20|

Agar teacher pooche

> Ali kis department mein hai?

To pehle

Student Table

↓

Department Table

Join karni padegi.

Har baar join lagegi.

Agar roz ye query chalti hai to system slow ho sakta hai.

To hum Department Name ko Student table mein hi rakh dete hain.

---

## Denormalized Table

| StudentID | Name | Department |
|-----------|------|------------|
|1|Ali|CS|
|2|Ahmed|IT|

Ab join ki zarurat hi nahi.

Query bohot fast chalegi.

---

# Lekin Problem?

Ab socho

Department "CS"

1000 students ke paas hai.

Agar naam change karna ho

Computer Science

To 1000 rows update karni hongi.

Ye redundancy hai.

---

# Denormalization ka Purpose

Denormalization sirf performance improve karne ke liye hoti hai.

Goal

✅ Fast Queries

❌ Perfect Normalization nahi

---

# Kab Denormalization Karni Chahiye?

Lecture ke mutabiq kuch situations hain.

---

# Situation 1

## One-to-One Relationship

Do tables agar hamesha saath use hoti hain to merge kar do.

Example

### Employee

|EmpID|Name|
|-----|----|
|1|Ali|

---

### Passport

|EmpID|PassportNo|
|------|-----------|
|1|AA12345|

Har baar dono tables join hoti hain.

To merge kar do.

---

|EmpID|Name|PassportNo|
|-----|----|-----------|
|1|Ali|AA12345|

Ab join nahi lagegi.

Performance improve hogi.

---

# Situation 2

## Many-to-Many Relationship

Ye exam ka important topic hai.

Suppose

Students

Courses

Ek student bohot courses le sakta hai.

Ek course bohot students le sakte hain.

Isliye teesri table banti hai.

```
Student

↓

Enrollment

↓

Course
```

Tables

---

Student

|ID|Name|
|--|----|
|1|Ali|

---

Course

|CourseID|Course|
|---------|------|
|CS101|DBMS|

---

Enrollment

|StudentID|CourseID|
|----------|--------|
|1|CS101|

---

Agar poocha jaye

Ali ka course kya hai?

To

Student

↓

Enrollment

↓

Course

Teen tables join hongi.

Ye expensive hai.

---

Solution

Enrollment ki information ko Course ya Student table mein merge kar do.

Ab sirf do tables join hongi.

---

# Situation 3

## Reference Data

Example

Student aur Hobby

---

Hobby Table

|ID|Hobby|
|--|------|
|1|Cricket|

---

Student

|ID|Name|HobbyID|
|--|----|--------|
|1|Ali|1|

Har baar Hobby ka naam chahiye.

Join lagti hai.

To Hobby Name Student table mein hi rakh do.

---

Student

|ID|Name|Hobby|
|--|----|------|
|1|Ali|Cricket|

Ab join khatam.

Performance fast.

---

# Advantages of Denormalization

| Advantage | Explanation |
|------------|-------------|
| Fast Queries | Joins kam hoti hain |
| Better Performance | Database jaldi response deta hai |
| Reporting Fast | Reports jaldi banti hain |
| Less Join Operations | CPU aur Memory kam use hoti hai |

---

# Disadvantages

| Disadvantage | Explanation |
|--------------|-------------|
| Data Redundancy | Same data repeat hota hai |
| Storage Zyada | Duplicate values save hoti hain |
| Update Problem | Ek value kai jagah update karni padti hai |
| Insert/Delete Anomalies | Data inconsistency aa sakti hai |

---

# Important Interview Question

## Kya hamesha Denormalization karni chahiye?

❌ Bilkul nahi.

Sirf tab jab

- Performance bohot slow ho
- Queries bohot joins use kar rahi hon
- Reports frequently chalti hon

---

# Partitioning

Ab doosra topic.

Denormalization mein

Tables Merge hoti hain.

Partitioning mein

Ek bari table ko divide kiya jata hai.

---

# Definition

Partitioning ka matlab hai

> Ek bari table ko chhoti chhoti tables (Partitions) mein divide karna.

---

# Example

Student Table

100 Million Records

Searching slow hogi.

To table ko divide kar do.

```
Student

↓

Partition 1

Partition 2

Partition 3

Partition 4
```

Ab search bohot fast hogi.

---

# Objectives of Partitioning

| Objective | Meaning |
|------------|---------|
| Workload Kam | Database par load kam hota hai |
| Balance Work | Har partition equal work kare |
| Speed | Search aur Access fast hota hai |

---

# Types of Partitioning

1. Horizontal Partitioning

2. Vertical Partitioning

---

# Horizontal Partitioning

Rows divide hoti hain.

Columns same rehte hain.

Example

Student Table

|ID|Name|
|--|----|
|1|Ali|
|2|Ahmed|
|3|Sara|
|4|Ayesha|

Divide

---

Partition 1

|ID|Name|
|--|----|
|1|Ali|
|2|Ahmed|

---

Partition 2

|ID|Name|
|--|----|
|3|Sara|
|4|Ayesha|

Columns same.

Rows divide.

---

# Vertical Partitioning

Columns divide hoti hain.

Rows same rehti hain.

Original Table

|ID|Name|Phone|Address|
|--|----|-----|--------|

Vertical Partition

Table 1

|ID|Name|
|--|----|

Table 2

|ID|Phone|Address|
|--|-----|--------|

Rows same.

Columns divide.

---

# Horizontal Partitioning ki Types

Lecture mein 3 types batayi gayi hain.

---

# 1. Range Partitioning

Rows ko ranges ke hisaab se divide karte hain.

Example

| Partition | Student IDs |
|------------|-------------|
|P1|1-1000|
|P2|1001-2000|
|P3|2001-3000|

Easy searching.

---

Problem

Ho sakta hai

P1

900 Records

P2

50 Records

Load equal nahi hoga.

---

# 2. Hash Partitioning

DBMS Hash Function use karta hai.

Formula automatically decide karta hai.

Example

```
Hash(StudentID)

↓

Partition Select
```

Benefit

Data almost equally distribute hota hai.

---

# 3. List Partitioning

Range nahi hoti.

List hoti hai.

Example

|Partition|Cities|
|----------|------|
|P1|Karachi, Hyderabad|
|P2|Lahore, Multan|
|P3|Islamabad, Peshawar|

Jis city ka naam hoga

Record us partition mein save hoga.

---

# Denormalization vs Partitioning

| Denormalization | Partitioning |
|-----------------|--------------|
| Tables Merge Hoti Hain | Table Divide Hoti Hai |
| Joins Kam Hoti Hain | Search Fast Hoti Hai |
| Redundancy Barh Sakti Hai | Redundancy Nahi Barhti |
| Performance Improve | Performance Improve |

---

# Real Life Example

## Denormalization

Hospital

Doctor aur Department har baar join hote hain.

Department Name Doctor table mein hi rakh diya.

Join khatam.

---

## Partitioning

Hospital mein

10 Million Patients hain.

Unhe Year ke hisaab se divide kar diya.

```
Patients_2023

Patients_2024

Patients_2025

Patients_2026
```

Ab search bohot fast.

---

# Exam Tips ⭐

## Difference

| Topic | Answer |
|--------|--------|
| Normalization | Tables Divide |
| Denormalization | Tables Merge |
| Partitioning | Table Divide into Parts |

---

## Yaad Rakhne ki Trick

🟢 **Normalization = Divide**

🟢 **Denormalization = Merge**

🟢 **Horizontal Partition = Rows Divide**

🟢 **Vertical Partition = Columns Divide**

🟢 **Range = Number Range**

🟢 **Hash = Formula**

🟢 **List = Fixed Values**

---

# Short Questions

### Q1. Denormalization kya hai?

**Answer:**
Performance improve karne ke liye normalized tables ko merge karna Denormalization kehlata hai.

---

### Q2. Denormalization kyun use hoti hai?

**Answer:**
- Fast queries
- Less joins
- Better performance

---

### Q3. Partitioning kya hai?

**Answer:**
Ek bari table ko chhoti partitions mein divide karna Partitioning kehlata hai.

---

### Q4. Horizontal Partitioning kya hoti hai?

**Answer:**
Rows ko divide karna Horizontal Partitioning kehlata hai.

---

### Q5. Vertical Partitioning kya hoti hai?

**Answer:**
Columns ko divide karna Vertical Partitioning kehlata hai.

---

# MCQs Practice

### 1. Denormalization ka main purpose kya hai?

A. Reduce Storage

B. Increase Redundancy

C. Improve Performance ✅

D. Delete Tables

---

### 2. Horizontal Partitioning kis basis par hoti hai?

A. Columns

B. Rows ✅

C. Keys

D. Index

---

### 3. Hash Partitioning kis cheez ka use karti hai?

A. Range

B. Formula (Hash Function) ✅

C. List

D. Join

---

### 4. List Partitioning mein kis cheez ka use hota hai?

A. Number Range

B. Fixed List of Values ✅

C. Formula

D. Index

---

# 📌 Final Summary

- **Normalization** data ko organize karti hai aur redundancy kam karti hai.
- **Denormalization** performance improve karne ke liye tables merge karti hai aur joins kam karti hai.
- **Partitioning** ek bari table ko chhoti partitions mein divide karti hai taake searching aur maintenance fast ho.
- **Horizontal Partitioning** rows ko divide karti hai.
- **Vertical Partitioning** columns ko divide karti hai.
- **Range Partitioning** ranges ke hisaab se, **Hash Partitioning** hash function ke through, aur **List Partitioning** fixed values ki list ke mutabiq data divide karti hai.

> 🎯 **Exam Trick:**  
> **Normalize = Divide Tables** → **Denormalize = Merge Tables** → **Partition = Divide One Big Table**
