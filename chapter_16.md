# Database Management System (CS403) – Lecture 16 Detailed Notes

# Mapping Relationships, Unary Relationships & Data Manipulation Languages

---

# Introduction

Pichli lectures mein hum ne Entity Types, Attributes, Relationships, Cardinality, Integrity Constraints aur Conceptual Database Design ko Relational Database Design mein convert karna seekha tha.

Is lecture mein hum detail se samjhenge:

- Mapping Relationships
- Binary Relationships
- Unary Relationships (Recursive Relationships)
- Supertype/Subtype Mapping
- Data Manipulation Languages (DML)
- Relational Algebra

---

# 1. Mapping Relationships

Jab hum Entity-Relationship (ER) Diagram ko Relational Database mein convert karte hain to sirf entities ko tables mein convert karna kaafi nahi hota.

Entities ke darmiyan jo relationships hoti hain unko bhi tables mein implement karna zaroori hota hai.

Isi process ko **Mapping Relationships** kehte hain.

---

## Relation vs Relationship

### Relation

Relational Database mein table ko Relation kehte hain.

### Example

| StudentID | StudentName |
|-----------|------------|
| 101 | Ali |
| 102 | Ahmed |

Ye ek Relation hai.

---

### Relationship

Do ya zyada relations ke darmiyan connection ko Relationship kehte hain.

### Example

```text
STUDENT -------- ENROLLS -------- COURSE
```

Yahan ENROLLS ek Relationship hai.

---

# 2. Binary Relationships

Binary Relationship wo relationship hoti hai jo sirf do entities ke darmiyan establish hoti hai.

---

## Types of Binary Relationships

### 1. One-to-One (1:1)

Ek record doosre table ke sirf ek record se relate ho sakta hai.

**Example:**

Student ↔ Scholarship Application

---

### 2. One-to-Many (1:M)

Ek record doosri table ke kai records se relate ho sakta hai.

**Example:**

Project ↔ Employees

---

### 3. Many-to-Many (M:N)

Dono tables ke records ek doosre ke kai records se relate ho sakte hain.

**Example:**

Students ↔ Books

---

# 3. One-to-Many Relationship (1:M)

Sab se common relationship hai.

---

## Real Life Example

### Department and Employees

Ek department mein kai employees kaam kar sakte hain.

Lekin ek employee sirf ek department mein kaam karta hai.

```text
Department (1) -------- (M) Employee
```

---

## Relational Model

### Department Table

```sql
DEPARTMENT(
    deptId PRIMARY KEY,
    deptName
)
```

### Employee Table

```sql
EMPLOYEE(
    empId PRIMARY KEY,
    empName,
    salary,
    deptId FOREIGN KEY
)
```

---

## Sample Data

### Department

| deptId | deptName |
|---------|----------|
| D1 | IT |
| D2 | HR |

### Employee

| empId | empName | deptId |
|--------|----------|---------|
| E1 | Ali | D1 |
| E2 | Ahmed | D1 |
| E3 | Sara | D2 |

---

## Important Rule

### One Side ki Primary Key ko Many Side mein Foreign Key banaya jata hai.

```text
One Side PK → Many Side FK
```

---

# 4. Minimum Cardinality

Minimum Cardinality batati hai ke relationship optional hai ya mandatory.

---

## Minimum Cardinality = 0

Optional Participation

Employee department ke baghair bhi exist kar sakta hai.

```sql
deptId NULL
```

---

## Minimum Cardinality = 1

Mandatory Participation

Employee ko zaroor kisi department se belong karna hoga.

```sql
deptId NOT NULL
```

---

## Real Life Example

### University Student

Har student ko kisi department mein hona zaroori hai.

```sql
departmentId NOT NULL
```

---

# 5. Many-to-Many Relationship (M:N)

Sab se important relationship hai.

---

## Real Life Example

### Students and Courses

Ek student kai courses le sakta hai.

Ek course kai students le sakte hain.

```text
STUDENT (M) ------ (M) COURSE
```

---

## Problem

Direct foreign key se relationship implement nahi ho sakti.

---

## Solution

Ek third table create ki jati hai.

Is table ko kehte hain:

- Associative Entity
- Junction Table
- Bridge Table

---

## Tables

### Student

```sql
STUDENT(
    stId PRIMARY KEY,
    stName
)
```

### Course

```sql
COURSE(
    courseId PRIMARY KEY,
    courseName
)
```

### Enrollment

```sql
ENROLLMENT(
    stId,
    courseId,
    enrollDate
)
```

---

## Sample Data

### Student

| stId | stName |
|------|---------|
| 1 | Ali |
| 2 | Ahmed |

### Course

| courseId | courseName |
|----------|------------|
| C1 | DBMS |
| C2 | OOP |

### Enrollment

| stId | courseId |
|------|-----------|
| 1 | C1 |
| 1 | C2 |
| 2 | C1 |

---

## Composite Primary Key

Enrollment table ki primary key:

```sql
(stId, courseId)
```

Isay Composite Primary Key kehte hain.

---

# 6. One-to-One Relationship (1:1)

---

## Real Life Example

Student aur Scholarship Application

Ek student sirf ek application de sakta hai.

Ek application sirf ek student ki hoti hai.

```text
STUDENT (1) -------- (1) APPLICATION
```

---

## Tables

### Student

```sql
STUDENT(
    stId PRIMARY KEY,
    stName
)
```

### Scholarship Application

```sql
APPLICATION(
    appId PRIMARY KEY,
    amount,
    stId FOREIGN KEY
)
```

---

## Sample Data

### Student

| stId | stName |
|-------|---------|
| 101 | Ali |
| 102 | Ahmed |

### Application

| appId | amount | stId |
|--------|---------|------|
| A1 | 50000 | 101 |

---

## Why Put FK in Application?

Har student application nahi deta.

Agar Application ID Student mein rakhen to bohat sari NULL values store hongi.

Storage waste hoga.

Isliye Student ki PK ko Application mein FK banaya jata hai.

---

# 7. Unary Relationships

Unary Relationship ko Recursive Relationship bhi kehte hain.

Is mein sirf ek entity relationship mein participate karti hai.

---

# Unary One-to-Many

## Real Life Example

Manager manages Employees

```text
EMPLOYEE
    |
MANAGES
    |
EMPLOYEE
```

---

## Table

```sql
EMPLOYEE(
    empId PRIMARY KEY,
    empName,
    managerId
)
```

---

## Sample Data

| empId | empName | managerId |
|--------|----------|-----------|
| 1 | Ali | NULL |
| 2 | Ahmed | 1 |
| 3 | Sara | 1 |

Ali manager hai.

Ahmed aur Sara us ke employees hain.

---

# Unary One-to-One

## Real Life Example

Roommate Relationship

Har student ka ek roommate ho sakta hai.

---

## Table

```sql
STUDENT(
    stId PRIMARY KEY,
    stName,
    roommateId
)
```

---

## Sample Data

| stId | stName | roommateId |
|------|---------|-----------|
| 1 | Ali | 2 |
| 2 | Ahmed | 1 |

---

# Unary Many-to-Many

## Real Life Example

Parts and Components

Ek machine kai parts se banti hai.

Ek part kai machines mein use ho sakta hai.

---

## Tables

### Part

```sql
PART(
    partId PRIMARY KEY,
    partName
)
```

### SubPart

```sql
SUBPART(
    partId,
    componentId
)
```

---

## Sample Data

### Part

| partId | partName |
|---------|----------|
| P1 | Car |
| P2 | Engine |
| P3 | Wheel |

### SubPart

| partId | componentId |
|---------|-------------|
| P1 | P2 |
| P1 | P3 |

Car Engine aur Wheels se mil kar bani hai.

---

# 8. Supertype and Subtype Mapping

## Real Life Example

Employee ek Supertype hai.

Employee ke types:

- Salaried Employee
- Hourly Employee
- Consultant

---

## Supertype Table

```sql
EMPLOYEE(
    empId PRIMARY KEY,
    empName,
    empAddress
)
```

---

## Salaried Employee

```sql
SALARIED_EMP(
    empId PRIMARY KEY,
    monthlySalary
)
```

---

## Hourly Employee

```sql
HOURLY_EMP(
    empId PRIMARY KEY,
    hourlyRate
)
```

---

## Consultant

```sql
CONSULTANT(
    empId PRIMARY KEY,
    contractAmount
)
```

---

## Discriminator

Ek special field jo subtype identify karti hai.

```sql
empType
```

Possible Values:

```text
S = Salaried
H = Hourly
C = Consultant
```

---

# 9. Mapping ER Diagram to Relational Database

### Step 1

Entities identify karo.

### Step 2

Har entity ko table mein convert karo.

### Step 3

Attributes add karo.

### Step 4

Primary Keys define karo.

### Step 5

Relationships identify karo.

### Step 6

Cardinality identify karo.

### Step 7

Foreign Keys implement karo.

### Step 8

Supertype/Subtype tables create karo.

---

# 10. Data Manipulation Languages (DML)

DML database ke data ko manage karne ke liye use hoti hai.

---

## Common Operations

### Insert

```sql
INSERT
```

### Update

```sql
UPDATE
```

### Delete

```sql
DELETE
```

### Retrieve

```sql
SELECT
```

---

# 11. Types of DML

## Procedural Languages

User ko batana padta hai:

1. Kya karna hai
2. Kaise karna hai

### Example

Relational Algebra

---

## Non-Procedural Languages

User sirf result batata hai.

Database khud decide karta hai ke result kaise nikala jaye.

### Example

```sql
SELECT * FROM STUDENT;
```

Ye SQL ka example hai.

---

# 12. Relational Algebra

Relational Algebra Relational Database ki Procedural Query Language hai.

---

## Important Properties

### 1. Input and Output Both are Relations

Input:

```text
STUDENT
```

Output:

```text
NEW RELATION
```

Original relation change nahi hoti.

---

### 2. Closure Property

Ek operation ka output doosri operation ka input ban sakta hai.

```text
Result1 → Result2 → Result3
```

---

## Five Basic Operations

### 1. Selection (σ)

Rows select karta hai.

```text
σ salary > 50000 (EMPLOYEE)
```

---

### 2. Projection (π)

Columns select karta hai.

```text
π empName (EMPLOYEE)
```

---

### 3. Cartesian Product (×)

Dono tables ke tamam combinations banata hai.

```text
STUDENT × COURSE
```

---

### 4. Union (∪)

Dono tables ka combined data.

```text
A ∪ B
```

---

### 5. Set Difference (-)

Ek table mein jo records hain aur doosri mein nahi.

```text
A - B
```

---

## Derived Operations

### Join

```text
STUDENT ⋈ COURSE
```

### Intersection

```text
A ∩ B
```

### Division

Complex query operations ke liye use hoti hai.

---

# Quick Revision

| Relationship Type | Implementation |
|------------------|---------------|
| One-to-One | PK of one table becomes FK in other |
| One-to-Many | PK of One Side becomes FK in Many Side |
| Many-to-Many | Third Table Created |
| Unary One-to-Many | Self Foreign Key |
| Unary Many-to-Many | Bridge Table |
| Supertype/Subtype | Separate Tables |
| Procedural Language | What + How |
| Non-Procedural Language | Only What |
| SQL | Non-Procedural |
| Relational Algebra | Procedural |

---

# Exam Important Points

✅ One-to-Many → PK goes to Many Side as FK

✅ Many-to-Many → Create Third Table

✅ Unary Relationship = Recursive Relationship

✅ Supertype PK appears in all Subtypes

✅ Discriminator identifies subtype

✅ SQL is Non-Procedural

✅ Relational Algebra is Procedural

✅ Five Basic Operations:

- Selection
- Projection
- Cartesian Product
- Union
- Difference
