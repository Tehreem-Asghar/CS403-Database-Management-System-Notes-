# Database Management System (CS403) - Lecture 15 Detailed Notes

# Database and Mathematical Relations

## Introduction

Pichli lecture mein hum ne Relational Data Model (RDM), tables ki properties aur mathematical relations ke concepts padhe thay. Is lecture mein hum database relations aur mathematical relations ke darmiyan farq, integrity constraints aur conceptual database design ko logical database design mein convert karna seekhenge.

---

# Database Relations vs Mathematical Relations

Database relation aur mathematical relation dono ki basic properties lag bhag same hoti hain.

## Similarities

- Rows ka order matter nahi karta.
- Duplicate tuples allowed nahi hotay.
- Relation ek set ki tarah behave karti hai.
- Har tuple unique hota hai.

## Main Difference

### Mathematical Relation

Mathematical relation mein columns ka order matter karta hai.

Example:

Set A = {Ali, Ahmed}

Set B = {20, 22}

A × B

| Name | Age |
|--------|--------|
| Ali | 20 |
| Ali | 22 |
| Ahmed | 20 |
| Ahmed | 22 |

B × A

| Age | Name |
|--------|--------|
| 20 | Ali |
| 20 | Ahmed |
| 22 | Ali |
| 22 | Ahmed |

Yahan:

A × B ≠ B × A

Is liye mathematical relation change ho jati hai.

---

### Database Relation

Database relation mein columns ka order change karne se relation nahi badalta.

Example:

Table 1

| StudentID | Name |
|------------|--------|
| S01 | Ali |

Table 2

| Name | StudentID |
|--------|------------|
| Ali | S01 |

Dono logically same relation hain.

---

# Degree of a Relation

## Definition

Relation mein columns (attributes) ki total tadaad ko Degree kehte hain.

---

## Example

STUDENT Table

| StudentID | Name | Class | Gender |
|------------|--------|--------|---------|
| S01 | Ali | BSCS | Male |
| S02 | Sara | BBA | Female |

Columns:

1. StudentID
2. Name
3. Class
4. Gender

Degree = 4

---

## Real Life Example

Employee Table

| EmpID | Name | Salary | Department | City |
|---------|---------|---------|------------|------|

Columns = 5

Degree = 5

---

# Cardinality of a Relation

## Definition

Relation mein rows (records) ki total tadaad ko Cardinality kehte hain.

---

## Example

STUDENT Table

| StudentID | Name |
|------------|--------|
| S01 | Ali |
| S02 | Ahmed |
| S03 | Sara |
| S04 | Fatima |

Rows = 4

Cardinality = 4

---

## Difference Between Degree and Cardinality

| Degree | Cardinality |
|----------|-------------|
| Number of Columns | Number of Rows |
| Vertical Count | Horizontal Count |

Example:

| ID | Name | Age |
|----|------|-----|
| 1 | Ali | 20 |
| 2 | Sara | 21 |
| 3 | Ahmed | 22 |

Degree = 3

Cardinality = 3

---

# Relation Keys

Keys relations mein records ko uniquely identify karne ke liye use hoti hain.

Types:

- Primary Key
- Candidate Key
- Alternate Key
- Composite Key
- Foreign Key

---

# Foreign Key

## Definition

Aisa attribute jo kisi doosri table ki Primary Key ho aur current table mein use ho raha ho, usay Foreign Key kehte hain.

---

## Example

### DEPARTMENT Table

| DeptID | DeptName |
|---------|----------|
| D01 | HR |
| D02 | IT |
| D03 | Finance |

Primary Key = DeptID

---

### EMPLOYEE Table

| EmpID | Name | DeptID |
|---------|--------|---------|
| E01 | Ali | D01 |
| E02 | Ahmed | D02 |
| E03 | Sara | D03 |

Primary Key = EmpID

Foreign Key = DeptID

---

## Real Life Example

University Database

### DEPARTMENT

| DeptID | Department |
|---------|------------|
| CS | Computer Science |
| SE | Software Engineering |

### STUDENT

| StudentID | Name | DeptID |
|------------|--------|---------|
| S01 | Ali | CS |
| S02 | Ahmed | SE |

DeptID student table mein foreign key hai.

---

# Foreign Key Rules

## Rule 1

Ek table mein:

- Zero Foreign Keys
- One Foreign Key
- Multiple Foreign Keys

ho sakti hain.

---

## Rule 2

Foreign Key ka Home Relation hota hai.

Example:

DEPARTMENT.DeptID → Primary Key

EMPLOYEE.DeptID → Foreign Key

DEPARTMENT Home Relation hai.

---

## Rule 3

Names different ho sakte hain.

Example:

DEPARTMENT

| DeptID |

EMPLOYEE

| DepartmentNumber |

Lekin data type same hona chahiye.

---

# Integrity Constraints

## Definition

Integrity Constraints database ki correctness aur consistency maintain karti hain.

Agar constraints na hon to database mein invalid data aa sakta hai.

---

# Entity Integrity Constraint

## Rule

Primary Key kabhi NULL nahi ho sakti.

---

## Example

Wrong

| StudentID | Name |
|------------|--------|
| NULL | Ali |

Allowed nahi.

---

## Correct

| StudentID | Name |
|------------|--------|
| S01 | Ali |

Allowed hai.

---

## Why?

Primary Key record ko uniquely identify karti hai.

Agar Primary Key NULL ho to record identify nahi ho sakta.

---

# Referential Integrity Constraint

## Rule

Foreign Key ki value:

- Ya parent table mein exist kare
- Ya NULL ho

---

## Correct Example

### DEPARTMENT

| DeptID |
|---------|
| D01 |
| D02 |

### EMPLOYEE

| EmpID | DeptID |
|---------|---------|
| E01 | D01 |
| E02 | D02 |

Valid Data

---

## Incorrect Example

### EMPLOYEE

| EmpID | DeptID |
|---------|---------|
| E03 | D99 |

D99 department exist nahi karta.

Constraint violate ho gayi.

---

## Real Life Example

Agar company mein IT department hi nahi hai aur kisi employee ko IT99 department assign kar diya jaye to data incorrect ho jayega.

Isi problem ko Referential Integrity prevent karti hai.

---

# Null Constraint

## Definition

NULL ka matlab:

- Value abhi available nahi
- Value abhi enter nahi ki gayi

---

## Example

| StudentID | Name | Fax |
|------------|--------|------|
| S01 | Ali | NULL |

Fax optional hai.

---

# NOT NULL Constraint

Agar attribute mandatory ho to NOT NULL lagate hain.

---

## Example

Bank Customer Table

| CNIC | Name | Address |
|-------|--------|---------|

CNIC aur Name mandatory hain.

Is liye:

CNIC → NOT NULL

Name → NOT NULL

---

# Default Value Constraint

## Definition

Agar user value enter na kare to predefined value automatically assign ho jaye.

---

## Example

Student Registration

| StudentID | Semester |
|------------|-----------|
| S01 | 1 |

Semester ki default value = 1

User enter na kare tab bhi automatically 1 save ho jayega.

---

## Real Life Example

Online Shopping

Status field:

Default Value = Pending

Order create hote hi status automatically Pending ho jata hai.

---

# Domain Constraint

## Definition

Attribute kis type ki values accept karega.

Isay Domain kehte hain.

---

## Examples

### Age

Allowed:

18

25

30

Not Allowed:

Ali

Karachi

---

### Name

Allowed:

Ali

Ahmed

Sara

Not Allowed:

123

45.5

---

### Date of Birth

Allowed:

01-01-2004

15-06-2003

Not Allowed:

Ali

500

---

# Importance of Domain Constraint

Wrong type ka data enter hone se bachata hai.

---

## Example

Age field mein:

Ali

enter nahi ho sakta.

Kyunkay Age numeric domain rakhta hai.

---

# Check Constraint

## Definition

Domain ko aur restrict karna.

---

## Example

Age ka data type:

BYTE

Range:

0 to 255

Lekin university rule:

Age <= 40

Constraint:

CHECK (Age <= 40)

---

## Real Life Example

Exam Marks

CHECK (Marks >= 0 AND Marks <= 100)

Student 150 marks enter nahi kar sakta.

---

# Relational Data Model Components

RDM ke 3 major components hain:

## 1. Structure

Tables

Columns

Rows

Keys

---

## 2. Integrity Constraints

- Entity Integrity
- Referential Integrity
- Domain Constraint

---

## 3. Manipulation Language

Data ko manipulate karna.

Examples:

- SELECT
- INSERT
- UPDATE
- DELETE

(SQL)

---

# Logical Database Design

## Definition

Conceptual Database Design ko Relational Model mein convert karna Logical Database Design kehlata hai.

---

# Design Process

### Step 1

Requirement Analysis

---

### Step 2

Entities Identify Karna

Example:

- Student
- Teacher
- Course

---

### Step 3

E-R Diagram Banana

---

### Step 4

Logical Database Design Banana

---

### Step 5

Tables Create Karna

---

# Transformation Rules

Conceptual Design → Logical Design

Do methods:

## Manual Conversion

Designer khud mapping karta hai.

---

## CASE Tools

Software automatically mapping karta hai.

Examples:

- Oracle Designer
- ERWin
- Visual Paradigm

---

# Mapping Entity Types

## Rule

Har Strong Entity Type directly table ban jati hai.

---

## Example

Entity

STUDENT

Attributes:

- StudentID
- Name
- DateOfBirth

Convert into:

STUDENT

| StudentID | Name | DateOfBirth |
|------------|--------|------------|

Primary Key:

StudentID

---

# Composite Attributes

## Definition

Aise attributes jo multiple sub-attributes se mil kar bane hon.

---

## Example

Name

- FirstName
- LastName

---

## Example

Address

- House Number
- Street Number
- City
- Country

---

# Transformation of Composite Attribute

Entity

Student

Address

- HouseNo
- StreetNo
- City
- Country

---

Convert into:

### STUDENT

| StudentID | Name |
|------------|--------|

### STUDENT_ADDRESS

| StudentID | HouseNo | StreetNo | City | Country |
|------------|---------|-----------|------|---------|

---

# Multi-Valued Attributes

## Definition

Aise attributes jin ki multiple values ho sakti hain.

---

## Example

Student Hobbies

Ali:

- Reading
- Cricket
- Gaming

Ek field mein multiple hobbies store karna relational model mein suitable nahi.

---

# Transformation Rule

Do tables banengi.

---

### STUDENT

| StudentID | Name |
|------------|--------|
| S01 | Ali |

---

### STUDENT_HOBBY

| StudentID | Hobby |
|------------|---------|
| S01 | Reading |
| S01 | Cricket |
| S01 | Gaming |

---

# Primary Key of Multi-Valued Attribute Table

Composite Key:

(StudentID, Hobby)

Example:

(S01, Reading)

(S01, Cricket)

(S01, Gaming)

Har row unique hai.

---

# Real Life Example

Customer Phone Numbers

Customer:

Ali

Phone Numbers:

- 03001234567
- 03111234567
- 03221234567

---

CUSTOMER

| CustomerID | Name |
|------------|--------|

CUSTOMER_PHONE

| CustomerID | PhoneNumber |
|------------|-------------|

---

# Lecture 15 Summary

Is lecture mein hum ne seekha:

✅ Database Relation aur Mathematical Relation ka difference

✅ Degree of Relation

✅ Cardinality of Relation

✅ Foreign Key aur us ke rules

✅ Entity Integrity Constraint

✅ Referential Integrity Constraint

✅ Null Constraint

✅ Default Value Constraint

✅ Domain Constraint

✅ Check Constraint

✅ Conceptual Design ko Logical Design mein transform karna

✅ Strong Entity Mapping

✅ Composite Attribute Transformation

✅ Multi-Valued Attribute Transformation

Ye tamam concepts database design aur SQL implementation ki foundation hain aur aage normalization aur database development mein bohat important role ada karte hain.
