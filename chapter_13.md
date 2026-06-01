# Lecture 13 – Examination System E-R Diagram (CS403)

# Overview

Is lecture mein hum Examination System ka **Conceptual Database Design** E-R Model ki madad se bananay ka process samajhte hain.

Topics Covered:

- Examination System ka E-R Diagram
- Conceptual Database Design
- Entity Types aur Attributes
- Relationships aur Cardinalities
- Derived Attributes
- Logical Database Design

---

# Introduction

Pichli lectures mein hum ne:

- System Analysis ki
- Requirements collect ki
- Data Flow Diagrams (DFDs) banaye

Ab hum Conceptual Design phase mein enter kar rahe hain jahan hum E-R Diagram ki madad se database structure design karenge.

E-R Diagram hume batata hai:

- System mein konsi entities hain
- Unke attributes kya hain
- Entities ek dusray se kis tarah related hain

---

# Major Entities of Examination System

Examination System mein following major entities hain:

1. Program
2. Student
3. Teacher
4. Course
5. Semester
6. Course Offered
7. Enrolled
8. Result

---

# 1. Program Entity

Program se murad degree programs hain.

Examples:

- BSCS
- BSIT
- BBA
- MBA
- MCS

## Attributes

| Attribute | Description |
|------------|-------------|
| pr_Code | Program Code |
| max_Dur | Maximum Duration |
| no_of_Semesters | Total Semesters |
| Pr_Lvl | Program Level |

### Example

| pr_Code | max_Dur | no_of_Semesters | Pr_Lvl |
|----------|----------|----------------|---------|
| BSCS | 4 Years | 8 | Undergraduate |
| MBA | 2 Years | 4 | Graduate |

## Primary Key

```text
pr_Code
```

Example:

```text
BSCS
MBA
MCS
```

---

# 2. Student Entity

Student ki personal aur academic information store karne ke liye.

## Attributes

| Attribute | Description |
|------------|-------------|
| Reg_No | Registration Number |
| st_Name | Student Name |
| st_Father_Name | Father's Name |
| st_Date_of_Birth | Date of Birth |
| st_Phone_No | Phone Number |
| st_GPA | GPA |
| st_Subj_Detail | Subject Details |

---

## Example

| Reg_No | Name |
|---------|---------|
| 2024-CS-001 | Ali |
| 2024-CS-002 | Ahmed |

---

## Primary Key

```text
Reg_No
```

Example:

```text
2024-CS-001
```

---

## Multi-Valued Attribute: GPA

Student ka GPA semester ke hisab se change hota hai.

Example:

| Student | Semester | GPA |
|----------|----------|------|
| Ali | Fall 2024 | 3.4 |
| Ali | Spring 2025 | 3.8 |

Isi wajah se GPA ko separate relation se handle kiya jata hai.

---

## Multi-Valued Attribute: Subject Detail

Har student ke multiple subjects hote hain.

Example:

| Student | Subject | Marks |
|----------|----------|--------|
| Ali | DBMS | 85 |
| Ali | OOP | 90 |

---

# 3. Teacher Entity

Teacher ki information store karne ke liye.

## Attributes

| Attribute | Description |
|------------|-------------|
| teacher_Reg_No | Registration Number |
| teacher_Name | Teacher Name |
| teacher_Father_Name | Father's Name |
| Qual | Qualification |
| Experience | Experience |
| teacher_Sal | Salary |

---

## Example

| Reg No | Name | Qualification |
|----------|---------|--------------|
| T001 | Dr. Khan | PhD |
| T002 | Dr. Ahmed | MS |

---

## Primary Key

```text
teacher_Reg_No
```

Example:

```text
T001
```

---

## Experience Attribute

Experience do tarah ka ho sakta hai.

### Single-Valued

```text
10 Years
```

### Multi-Valued

| Institute | Experience |
|------------|------------|
| ABC College | 3 Years |
| XYZ University | 7 Years |

---

# Common Attributes Between Student and Teacher

Dono entities mein kuch common attributes hain:

- Name
- Father Name
- Address
- Phone Number

Real-world systems mein inhe inheritance ke through bhi model kiya ja sakta hai.

---

# 4. Course Entity

Institute ke subjects ko represent karta hai.

Examples:

- DBMS
- OOP
- Networking
- AI
- Data Structures

---

## Attributes

| Attribute | Description |
|------------|-------------|
| course_Code | Course Code |
| course_Name | Course Name |
| course_Prereq | Prerequisite Courses |
| Courses_Offered_In | Offered Program/Semester |

---

## Example

| course_Code | course_Name |
|-------------|-------------|
| CS3207 | DBMS |
| CS3208 | Networking |

---

## Primary Key

```text
course_Code
```

---

# Recursive Relationship

## course_Prereq

Kuch courses ke prerequisites hote hain.

Example:

```text
Networking
```

Prerequisites:

```text
Data Structures
Operating Systems
```

Diagram:

```text
COURSE
   |
Prerequisite
   |
COURSE
```

Yeh Recursive Relationship hai kyun ke Course ka relation Course se hi hai.

---

# Courses Offered In

Kisi course ko offer karne ke liye Program aur Semester dono required hain.

Example:

| Course | Program | Semester |
|----------|----------|-----------|
| DBMS | BSCS | 4th |
| OOP | BSCS | 3rd |

---

# 5. Semester Entity

Semester ki information store karne ke liye.

---

## Attributes

| Attribute | Description |
|------------|-------------|
| semester_Name | Semester Name |
| semester_Start_Date | Start Date |
| semester_End_Date | End Date |

---

## Example

| Semester | Start Date | End Date |
|------------|------------|----------|
| Fall 2024 | Aug 2024 | Dec 2024 |
| Spring 2025 | Jan 2025 | May 2025 |

---

## Primary Key

```text
semester_Name
```

Example:

```text
Fall 2024
Spring 2025
```

---

# Derived Attributes

Derived Attributes directly store nahi kiye jate.

Ye dusre data se calculate hote hain.

---

## CGPA

CGPA semesters ke GPA se calculate hota hai.

Example:

| Semester GPA |
|-------------|
| 3.4 |
| 3.6 |
| 3.8 |

Formula:

```text
CGPA = Average of All Semester GPAs
```

---

## Semester GPA

Semester GPA subjects ke GPA se calculate hota hai.

Example:

| Subject | GPA |
|----------|------|
| DBMS | 3.5 |
| OOP | 3.7 |
| AI | 3.9 |

---

# Relationships and Cardinalities

Sab se important section.

Cardinality batati hai:

```text
Minimum participation
Maximum participation
```

---

# 1. Program and Course Relationship

Question:

```text
BSCS mein kon kon se courses hain?
```

---

## Cardinality

```text
PROGRAM (1) -------- (*) COURSE
```

Meaning:

Ek Program ke paas:

- Minimum 1 Course
- Maximum Many Courses

Example:

BSCS:

- DBMS
- OOP
- AI
- Networking

---

## Reverse Side

```text
COURSE (0..*) -------- PROGRAM
```

Meaning:

Course temporarily kisi Program mein na bhi ho sakta hai.

Example:

```text
Cloud Computing
```

Course create ho gaya hai lekin abhi kisi program mein assign nahi hua.

---

# 2. Student and Program Relationship

## Cardinality

```text
STUDENT (1) -------- (1) PROGRAM
```

Meaning:

Har Student sirf ek Program mein enrolled hota hai.

Example:

```text
Ali → BSCS
Ahmed → BBA
```

---

## Reverse Side

```text
PROGRAM (0..*) -------- STUDENT
```

Meaning:

Ek Program mein:

- Zero Students
- Ya Multiple Students

ho sakte hain.

---

# 3. Semester and Course Relationship

Question:

```text
Konsa Course kis Semester mein offer hua?
```

---

## Cardinality

```text
SEMESTER (*) -------- (*) COURSE
```

Many-to-Many

Example:

### Fall 2024

- DBMS
- OOP

### Spring 2025

- DBMS
- Networking

DBMS dono semesters mein offer hua.

---

# Course Offered Entity

Many-to-Many relationship ko break karne ke liye.

Entity:

```text
COURSE_OFFERED
```

Composite Key:

```text
semester_Name
+
course_Code
```

Example:

| Semester | Course |
|-----------|---------|
| Fall 2024 | DBMS |
| Spring 2025 | DBMS |

---

# 4. Course Offered and Teacher Relationship

## Cardinality

```text
TEACHER (1) -------- (*) COURSE_OFFERED
```

Meaning:

Ek teacher multiple courses padha sakta hai.

Example:

Dr. Khan:

- DBMS
- OOP
- AI

---

## Reverse Side

```text
COURSE_OFFERED (1) -------- TEACHER
```

Har offered course ka ek responsible teacher hoga.

---

# 5. Student and Course Offered Relationship

Question:

```text
Kis student ne konsa course enroll kiya?
```

Many-to-Many Relationship.

---

# Enrolled Entity

Entity:

```text
ENROLLED
```

Composite Key:

```text
Reg_No
+
Course_Code
+
Semester_Name
```

Example:

| Student | Course | Semester |
|----------|---------|-----------|
| Ali | DBMS | Fall 2024 |
| Ali | OOP | Fall 2024 |

---

# 6. Student and Semester Relationship

Question:

```text
Kisi semester mein student ka GPA kya tha?
```

Many-to-Many Relationship.

---

# Result Relationship

Attribute:

```text
GPA
```

Example:

| Student | Semester | GPA |
|----------|----------|------|
| Ali | Fall 2024 | 3.5 |
| Ali | Spring 2025 | 3.8 |

---

# Complete Conceptual Model

```text
PROGRAM
   |
   | 1:M
   |
COURSE
   |
   | M:M
   |
COURSE_OFFERED
   |
   | M:1
   |
TEACHER

COURSE_OFFERED
      |
      | M:M
      |
   ENROLLED
      |
      |
   STUDENT
      |
      | M:M
      |
    RESULT
      |
      |
   SEMESTER
```

---

# Conceptual Database Design

Analysis phase ka final output:

```text
Conceptual Database Design
```

Features:

- DBMS Independent
- Tool Independent
- Business Requirements Based

Is stage par sirf system ki structure define ki jati hai.

---

# Logical Database Design

Agla phase:

```text
Logical Database Design
```

Yahan hum data model select karte hain.

Example:

- Relational Model
- Network Model
- Hierarchical Model

CS403 mein hum:

```text
Relational Data Model
```

use karenge.

---

# Real-World Example

University System

Programs:

- BSCS
- BBA

Students:

- Ali
- Ahmed

Courses:

- DBMS
- OOP

Semester:

- Fall 2024

Teacher:

- Dr. Khan

Scenario:

```text
Ali BSCS mein enrolled hai.

Fall 2024 mein Ali ne:
DBMS aur OOP liya.

Dr. Khan ne DBMS parhaya.

Semester ke end par:
Ali ka GPA = 3.6

CGPA baad mein tamam GPAs ko combine karke calculate kiya gaya.
```

---

# Key Exam Points

✔ Program ki Primary Key = pr_Code

✔ Student ki Primary Key = Reg_No

✔ Teacher ki Primary Key = teacher_Reg_No

✔ Course ki Primary Key = course_Code

✔ Semester ki Primary Key = semester_Name

✔ GPA Multi-Valued Attribute hai

✔ Subject Detail Multi-Valued Attribute hai

✔ Course Prerequisite Recursive Relationship hai

✔ Course Offered Associative Entity hai

✔ Enrolled Associative Entity hai

✔ CGPA Derived Attribute hai

✔ Conceptual Design Tool Independent hoti hai

✔ Logical Design Data Model Dependent hoti hai

✔ Many-to-Many relationships ko associative entities ke through implement kiya jata hai

---
# End of Lecture 13 Notes
