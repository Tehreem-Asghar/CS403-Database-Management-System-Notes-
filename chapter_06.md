# Lecture No. 06

# Topics Covered

- Detailed DFD Diagrams
- Database Design Phase
- Data Models
- Types of Data Models
- Types of Database Designs

---

# Detailed DFD Diagrams

Detailed DFD (Data Flow Diagram) us waqt use hota hai jab hume Level 0 Diagram ke kisi process ko mazeed detail me explain karna ho.

Ye diagram un processes ki internal working ko show karta hai jo Level 0 DFD me briefly explain kiye gaye hote hain.

## Important Points

- Detailed DFD optional hota hai
- Sirf un processes ke liye banaya jata hai jin ki detail required ho
- Is me same symbols use hote hain jo dusre DFDs me use hote hain
- Sub-process numbering hierarchical hoti hai

## Process Numbering Example

Agar Level 0 process:

```text
1.0
```

ho to us ke sub-processes:

```text
1.1
1.2
1.3
```

hongay.

Agar process 1.2 ki further detail banani ho to:

```text
1.2.1
1.2.2
1.2.3
```

numbering use hogi.

---

# Real Life Example of Detailed DFD

## ATM System

### Level 0 Process

```text
1.0 Withdraw Cash
```

### Detailed DFD

```text
1.1 Verify Card
1.2 Check Balance
1.3 Dispense Cash
1.4 Print Receipt
```

---

# Database Design Phase

Database Design Phase analysis phase ke baad aati hai.

Is phase me database ki structure design ki jati hai taake users ki requirements efficiently fulfill ho saken.

## Main Purpose

- Data organize karna
- Relationships define karna
- Efficient database banana

---

# Real Life Example

School Management System me:

- Students
- Teachers
- Courses
- Results

ki tables aur relationships design karna database design phase ka part hai.

---

# Data Models

Data Model ek framework hota hai jo database design create karne ke liye use hota hai.

Ye define karta hai:

- Data kis tarah store hoga
- Data ko manipulate kaise karenge
- Constraints kya hongi

---

# Components of Data Model

## 1. Structure

Data kis form me store hoga.

### Example

- Tables
- Records
- Objects

---

## 2. Manipulation Language

Data ko manipulate karne wali language.

### Example

```sql
SELECT * FROM Students;
```

---

## 3. Integrity Constraints

Rules jo data ki correctness maintain karte hain.

### Example

- Primary Key
- Foreign Key
- NOT NULL

---

# Types of Data Models

Data Models ki do major categories hoti hain:

## 1. Semantic Data Models

Ye better flexibility aur meaningful relationships provide karte hain.

### Types

- ER Data Model
- Object Oriented Data Model

---

# ER Data Model Example

```text
Student ---- Enrolls ---- Course
```

---

## 2. Record Based Data Models

Ye records ki form me data store karte hain.

### Types

- Hierarchical Data Model
- Network Data Model
- Relational Data Model

---

# Hierarchical Model Example

```text
University
   └── Department
         └── Teacher
```

---

# Network Model Example

```text
Student ←→ Course
```

---

# Relational Model Example

| studentId | studentName |
|---|---|
| 1 | Ali |

---

# Types of Database Designs

Database Design ki 3 main levels hoti hain:

## 1. Conceptual Database Design

High-level design hoti hai.

### Example

ER Diagram banana.

---

## 2. Logical Database Design

Conceptual design ko tables me convert karna.

### Example

Students table create karna.

---

## 3. Physical Database Design

Database ko actual DBMS me implement karna.

### Example

MySQL me tables create karna.

```sql
CREATE TABLE Students(
    studentId INT PRIMARY KEY,
    studentName VARCHAR(50)
);
```

---

# Benefits of Separate Database Design Levels

- Better abstraction
- Easy understanding
- Flexibility
- Easy DBMS migration

---

# Summary

- Detailed DFD processes ki detailed working show karta hai
- Database Design Phase database structure create karti hai
- Data Model database designing ka framework hota hai
- Semantic aur Record Based models important categories hain
- Database Design ki 3 levels hoti hain:
  - Conceptual
  - Logical
  - Physical
