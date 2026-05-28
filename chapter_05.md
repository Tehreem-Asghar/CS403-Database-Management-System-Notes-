# Lecture No. 05 — Database System Development & DFD Notes

# Introduction

Database Design aur Database Application Design dono closely related concepts hain.  
Database design ka main purpose ek aisa system banana hota hai jo organization ke data ko efficiently store, manage aur retrieve kar sake.

Database Application Development Process mein:
- Database Design
- Application Development
- Implementation

parallel bhi chal sakte hain.

---

# Database Application Development Process

Database application development ke major stages:

1. Preliminary Study
2. Requirement Analysis
3. Database Design
4. Physical Design
5. Implementation
6. Maintenance

---

# 1. Preliminary Study

Is phase mein poore organization ko study kiya jata hai.

Hum analyze karte hain:
- Different departments
- Information flow
- Processing activities
- Department interactions

## Real Life Example

Agar hum **University Management System** bana rahe hain to:

Departments:
- Admission Department
- Accounts Department
- Examination Department
- Library

Hum dekhte hain:
- Student data kahan se aata hai
- Fee verification kahan hoti hai
- Result kis department se generate hota hai

---

# 2. Requirement Analysis

Is phase mein detailed requirements collect ki jati hain.

Methods:
- Interviews
- Observation
- Documentation

## Example

Student Management System mein:
- Student registration chahiye
- Fee management chahiye
- Result generation chahiye
- Attendance system chahiye

---

# 3. Database Design

Is phase mein logical database structure create hota hai.

Activities:
- Entities identify karna
- Attributes define karna
- Relationships create karna

## Example

### Entity: Student

| Attribute | Description |
|---|---|
| StudentID | Unique ID |
| Name | Student Name |
| Department | Student Department |

### Entity: Course

| Attribute | Description |
|---|---|
| CourseID | Course ID |
| CourseName | Course Name |

### Relationship

Student enrolls in Course

---

# 4. Physical Design

Logical design ko actual DBMS mein implement kiya jata hai.

## Important Tasks

- Data Types select karna
- Tables create karna
- Indexes banana
- Storage structure define karna

## Example

DBMS:
- MySQL
- Oracle
- SQL Server

---

# 5. Implementation

Is phase mein applications develop ki jati hain.

## Example

University System Applications:
- Student Portal
- Teacher Portal
- Admin Panel

---

# 6. Maintenance

Maintenance ka purpose:
- Errors remove karna
- Performance improve karna
- New features add karna

## Example

Agar result calculation mein bug ho to usay fix kiya jata hai.

---

# Tools Used for Database System Development

## Tools Kyun Use Kiye Jate Hain?

Tools standard design notation provide karte hain.

Agar tools na hon:
- Har designer apni notation use karega
- Dusre designers confuse ho sakte hain

Tools:
- Communication easy banate hain
- Design ko understandable banate hain
- User aur designer ke darmiyan agreement mein help karte hain

---

# Data Flow Diagram (DFD)

DFD database systems design karne ka sabse common tool hai.

## DFD Kya Show Karta Hai?

- Data ka flow
- Processes
- Storage
- External entities

DFD:
- Simple hota hai
- Complexities hide karta hai
- Graphical representation provide karta hai

---

# Limitation of DFD

DFD:
- Decision points show nahi karta
- Sirf data flow par focus karta hai

---

# Symbols Used in DFD

---

# 1. Data Flow Symbol

## Purpose

Data movement show karta hai.

## Symbol

```text
 ---------->
```

## Example

```text
Student Form ---------> Admission Department
```

---

# 2. Data Store Symbol

## Purpose

Data ko store karne ke liye use hota hai.

## Symbol

```text
|| Student Record ||
```

## Example

```text
|| Fee Data ||
```

---

# 3. Process Symbol

## Purpose

Data ko process ya transform karta hai.

## Symbol

```text
 ( Process )
```

ya

```text
[ Process ]
```

## Example

```text
( Calculate Result )
```

---

# 4. External Entity Symbol

## Purpose

System ke bahar ki entity show karta hai.

## Symbol

```text
+-----------+
|  Student  |
+-----------+
```

## Example

- Student
- Teacher
- Bank

---

# 5. Collector Symbol

## Purpose

Multiple data flows ko ek point par collect karta hai.

## Symbol

```text
 \ | /
  \|/
   V
```

## Example

Different departments ka data central database mein jana.

---

# 6. Separator Symbol

## Purpose

Ek source se multiple destinations tak data bhejna.

## Symbol

```text
   ^
  /|\
 / | \
```

## Example

Result:
- Student ko
- Admin ko
- Examination department ko

---

# 7. Ring Sum Operator

## Purpose

Data sirf ek destination ki taraf jata hai.

## Symbol

```text
 ---(O)---
```

## Example

Payment:
- Cash
ya
- Online

---

# 8. AND Operator

## Purpose

Data sab destinations ki taraf jata hai.

## Symbol

```text
 ---(+)---
```

## Example

Registration data:
- Accounts ko bhi
- Library ko bhi
- Examination ko bhi

---

# Types of DFD

1. Context Diagram
2. Level 0 Diagram
3. Detailed Diagram

---

# 1. Context Diagram

Sabse basic DFD hota hai.

## Features

- Sirf ek process
- Internal details nahi hoti
- External entities show hoti hain
- Data stores nahi hote

---

# Context Diagram Example

```text
+-----------+        Student Data       +----------------------+
|  Student  | -----------------------> | University System    |
+-----------+                          +----------------------+

+-----------+ <----------------------- +----------------------+
|  Teacher  |       Reports            | University System    |
+-----------+                          +----------------------+
```

---

# 2. Level 0 DFD

Ye system ki detailed working show karta hai.

## Features

- Multiple processes
- Data stores
- External entities
- Internal processing

---

# Level 0 DFD Example

```text
+-----------+
|  Student  |
+-----------+
      |
      v
(1.0 Registration Process)
      |
      v
|| Student Database ||

      |
      v
(2.0 Fee Verification)
      |
      v
|| Fee Database ||

      |
      v
(3.0 Result Generation)
      |
      v
+-----------+
|  Teacher  |
+-----------+
```

---

# Detailed Diagram

Detailed DFD kisi complex process ko further explain karta hai.

## Example

Process 1.0 ko divide karna:

```text
1.0 Registration Process

1.1 Receive Form
1.2 Verify Documents
1.3 Store Student Data
```

---

# Steps for Creating Level 0 DFD

## Step 1 — Modules Identify Karna

Example:
- Admission
- Accounts
- Examination

---

## Step 2 — Har Module ka DFD Banana

Har module ki working show karna.

---

## Step 3 — DFDs Ko Connect Karna

Processes aur data stores ko connect karna.

---

## Step 4 — Numbering Karna

Example:

```text
1.0 Registration
1.1 Verify Form
1.2 Save Record
```

---

# Important Points

- DFD graphical representation hota hai
- Data movement ko show karta hai
- Easy understanding provide karta hai
- Large systems ko manageable banata hai
- Database design mein bohat important tool hai

---

# Real Life Example — ATM System DFD

## Context Diagram

```text
+---------+       Withdraw Request      +-------------+
| Customer| --------------------------> | ATM System  |
+---------+                             +-------------+

+---------+ <-------------------------- +-------------+
| Customer|         Cash                | ATM System  |
+---------+                             +-------------+
```

---

# Real Life Example — Library System

## Processes

- Issue Book
- Return Book
- Fine Calculation

## Data Stores

- Book Database
- Student Database

## External Entities

- Student
- Librarian

---

# Conclusion

Database system development ek structured process hai jisme:
- Planning
- Analysis
- Design
- Implementation
- Maintenance

sab phases important hote hain.

DFD ek powerful graphical tool hai jo:
- System ko visualize karta hai
- Data flow show karta hai
- Complex systems ko easy banata hai

Isi wajah se DFD database designing mein extensively use hota hai.
