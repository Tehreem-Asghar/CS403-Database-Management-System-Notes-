# Lecture 10 - Cardinality Types, Roles, Dependencies, Supertype & Subtype (Roman Urdu Notes)

# Introduction

Is lecture mein hum ER (Entity Relationship) Model ke kuch advanced concepts parh rahe hain:

- Cardinality Types
- Roles in Relationships
- Dependencies
- Existence Dependency
- Identifier Dependency
- Referential Dependency
- Supertype and Subtype Entities

Ye concepts database ko accurately design karne ke liye bohat important hain.

---

# Cardinality

Cardinality batati hai ke ek entity ke kitne instances doosri entity ke sath relationship mein aa sakte hain.

Simple words mein:

"Ek record doosri table ke kitne records se relate ho sakta hai?"

---

# Types of Cardinality

Cardinality ke do important parts hote hain:

## 1. Maximum Cardinality

Maximum Cardinality batati hai ke:

> Kisi entity ka ek instance doosri entity ke kitne maximum instances ke sath associate ho sakta hai.

### Example

Ek Student maximum 6 books issue kar sakta hai.

Yahan maximum cardinality = 6

---

## 2. Minimum Cardinality

Minimum Cardinality batati hai ke:

> Kisi entity ka ek instance kam az kam kitne instances ke sath associate hona chahiye.

Yeh relationship ki compulsory ya optional nature ko show karti hai.

### Values

| Value | Meaning |
|---------|---------|
| 0 | Optional |
| 1 | Mandatory |

---

# Optional Relationship

Jab minimum cardinality 0 ho.

Matlab relationship hona zaroori nahi.

### Example

Student aur Hobby

Student hobby rakhta bhi ho sakta hai aur nahi bhi.

```text
Student (0...1) Hobby
```

---

# Mandatory Relationship

Jab minimum cardinality 1 ho.

Matlab relationship zaroor hona chahiye.

### Example

Employee aur Project

Har employee ko kam az kam ek project assign hona zaroori hai.

```text
Employee (1...Many) Project
```

---

# One-to-Many Relationship (1:M)

Sab se common cardinality.

### Rule

Ek entity ka ek instance doosri entity ke kai instances ke sath relate ho sakta hai.

---

## Real Life Example

Department aur Employees

```text
Department
    |
    | 1
    |
    | M
Employees
```

### Explanation

Ek Department:

- HR

Kai Employees:

- Ali
- Ahmed
- Sara
- Bilal

Ek department mein kai employees ho sakte hain.

---

# Many-to-One Relationship (M:1)

One-to-Many ka reverse hota hai.

---

## Real Life Example

Employees aur Department

```text
Employees
     |
     | M
     |
     | 1
Department
```

Kai employees ek department se belong kar sakte hain.

---

# Many-to-Many Relationship (M:N)

Dono entities ke multiple records ek doosray ke sath associate ho sakte hain.

---

## Real Life Example

Students aur Courses

```text
Student
    |
    | M
    |
    | N
Course
```

### Example

Ali:

- Database
- Programming
- Networking

Database Course:

- Ali
- Ahmed
- Sara

---

# Cardinality Example 1

## Student and Book

Library System

```text
Student -------- Book
```

### Rules

Student:

- Book issue kare ya na kare.

Book:

- Kai students issue kar sakte hain.

### Real Example

Ali:

- Database Book
- Java Book
- Python Book

Ahmed:

- No Book

Isliye minimum cardinality student side par 0 hai.

---

# Cardinality Example 2

## Employee and Project

```text
Project -------- Employee
```

### Rules

Ek project:

- Kai employees rakh sakta hai.

Employee:

- Kam az kam ek project par hona chahiye.

### Example

Project:

Online Shopping System

Employees:

- Ali (Developer)
- Sara (Designer)
- Ahmed (Tester)

---

# Cardinality Example 3

## Student and Course

```text
Student -------- Course
```

### Rules

Student:

- Kai courses le sakta hai.

Course:

- Kai students le sakte hain.

### Example

Ali:

- Database
- Programming

Database:

- Ali
- Ahmed
- Bilal

Yeh Many-to-Many relationship hai.

---

# Cardinality Example 4

## Student and Hobby

```text
Student -------- Hobby
```

### Rules

Student:

- Hobby ho bhi sakti hai
- Hobby na bhi ho sakti hai

Hobby:

- Kai students ki same hobby ho sakti hai

### Example

Cricket:

- Ali
- Ahmed
- Bilal

---

# ER Diagram Notations

ER Diagrams ko draw karne ke kai methods hain.

---

# 1. Crow's Foot Notation

Sab se famous notation.

```text
One = |
Many = < crow foot >
```

Example:

```text
Department |----< Employee
```

---

# 2. Arrow Head Notation

Is notation mein arrows use hote hain.

### Rules

Single Arrow = One

Double Arrow = Many

---

### Example

```text
Department --> Employees
```

One Department

Many Employees

---

# 3. Alphabetical Notation

Numbers aur alphabets use hote hain.

### Rules

```text
1 = One

M = Many

N = Many
```

Example:

```text
Department 1 ----- M Employee
```

---

# 4. Dot Based Notation

### Rules

```text
1 = One

● = Many
```

Example:

```text
Department 1 ----- ● Employee
```

---

# Roles in Relationships

Role batata hai ke entity relationship mein kis capacity mein participate kar rahi hai.

Role relationship ka meaning clear karta hai.

---

# Situations Where Roles Are Necessary

## 1. Recursive Relationship

## 2. Multiple Relationships

---

# Recursive Relationship

Jab ek entity khud apne sath relationship banaye.

Isay Unary Relationship bhi kehte hain.

---

## Example

Faculty aur Head Faculty

```text
Faculty
   |
 Heads
   |
Faculty
```

### Real Life Example

Computer Science Department

Faculty Members:

- Dr Ahmed
- Dr Sara
- Dr Bilal

Dr Ahmed department head hain.

Yahan Head bhi Faculty hai aur members bhi Faculty hain.

---

# Multiple Relationships

Jab do entities ke darmiyan aik se zyada relationships hon.

---

## Example

Faculty aur Student

### Relationship 1

Faculty teaches Student

### Relationship 2

Faculty supervises Student

```text
Faculty ---- Teaches ---- Student

Faculty ---- Supervises ---- Student
```

---

## Real Example

Dr Ahmed:

- Database parhate hain
- Final Year Project supervise karte hain

Isliye roles mention karna zaroori hai.

---

# Dependencies

Dependency bhi ek constraint hai.

Dependency batati hai ke ek entity doosri entity par kitni depend hai.

---

# Types of Dependencies

1. Existence Dependency

2. Identifier Dependency

3. Referential Dependency

---

# Existence Dependency

Jab ek entity ki existence doosri entity par depend kare.

---

## Real Life Example

Employee aur Project

```text
Project ---- Employee
```

Agar employee kisi project par assign hi nahi hai to employee record valid nahi hoga.

Employee project par depend hai.

---

# Identifier Dependency

Jab dependent entity ka apna identifier na ho.

Parent entity ki key use ki jaye.

---

## Example

Order

```text
OrderID
```

Order Item

```text
OrderID + ItemNo
```

Yahan OrderID parent entity se aa raha hai.

---

# Referential Dependency

Jab dependent entity ka apna identifier bhi ho aur foreign key bhi.

---

## Real Life Example

Book aur Copies

Book:

```text
BookID
BookTitle
```

Copy:

```text
CopyID
BookID
```

BookID foreign key hai.

---

## Example Data

Book

```text
BookID = 101

Database Systems
```

Copies

```text
CopyID = 1
BookID = 101

CopyID = 2
BookID = 101
```

Agar BookID 101 wali book delete ho jaye to copies bhi invalid ho jayengi.

Yeh Referential Dependency hai.

---

# Foreign Key

Foreign Key parent table ki Primary Key hoti hai jo child table mein store ki jati hai.

---

## Example

Book Table

```text
BookID (PK)
Title
```

Copy Table

```text
CopyID (PK)
BookID (FK)
```

BookID yahan Foreign Key hai.

---

# Enhancements in ER Model

Basic ER Model ko aur powerful banane ke liye kuch enhancements add ki gayi hain.

Sab se important enhancement:

- Supertype
- Subtype

---

# Supertype

General entity ko Supertype kehte hain.

---

## Example

```text
PERSON
```

Common Attributes:

- Name
- Age
- Address

---

# Subtype

Specialized entities ko Subtype kehte hain.

---

## Example

```text
PERSON
   |
----------------
|              |
Student      Faculty
```

Student aur Faculty dono Person hain.

---

# Real Life Example

PERSON

Common Attributes:

```text
Name
Gender
Age
Address
```

---

## Student

Extra Attributes

```text
Roll Number
Semester
CGPA
```

---

## Faculty

Extra Attributes

```text
Employee ID
Designation
Salary
```

---

# Multi-Level Specialization

```text
PERSON
   |
----------------
|              |
Student      Faculty
   |
-----------------
|       |       |
BSCS   BSSE   BBA
```

---

# Understanding Generalization

Jab multiple similar entities ko combine karke ek common entity banayi jaye.

Example:

```text
Student
Teacher
Employee
```

Combine →

```text
PERSON
```

Is process ko Generalization kehte hain.

---

# Understanding Specialization

Jab ek general entity ko further divide kiya jaye.

Example:

```text
PERSON
```

Divide →

```text
Student
Faculty
```

Is process ko Specialization kehte hain.

---

# Complete Lecture Summary

Is lecture mein hum ne seekha:

- Cardinality
- Maximum Cardinality
- Minimum Cardinality
- Optional Relationship
- Mandatory Relationship
- One-to-Many
- Many-to-One
- Many-to-Many
- Crow's Foot Notation
- Arrow Head Notation
- Alphabetical Notation
- Dot Based Notation
- Roles in Relationships
- Recursive Relationships
- Multiple Relationships
- Dependencies
- Existence Dependency
- Identifier Dependency
- Referential Dependency
- Foreign Key
- Supertype
- Subtype
- Generalization
- Specialization

Ye tamam concepts ER Model aur Database Design ko samajhne ke liye bohat important hain aur practical database systems mein roz use hote hain.
