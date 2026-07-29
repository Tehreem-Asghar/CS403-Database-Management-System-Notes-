# Database Management System (CS403) – Lecture 21
# Normalization Summary, Normalization Example & Physical Database Design (Complete Notes)

> **Goal of this Lecture**
>
> Is lecture ka maqsad hai:
>
> - Normalization ko revise karna
> - Ek complete example ke through Normalization samajhna
> - Physical Database Design ka introduction lena

---

# 1. Normalization Revision

## Normalization Kya Hai?

Normalization ek **step-by-step process** hai jo database ko organize karta hai taake:

- Data duplication kam ho.
- Data consistent rahe.
- Database maintain karna easy ho.
- Insert, Update aur Delete problems na aayein.

Simple words mein:

> **Normalization ka matlab database ko itna organize karna hai ke har information sirf aik jagah store ho.**

---

# Example

## Without Normalization

| StudentID | StudentName | Course | Teacher |
|-----------|-------------|---------|----------|
|101|Ali|DBMS|Ahmed|
|101|Ali|OOP|Kashif|
|101|Ali|AI|Sara|

Problem:

Student Name "Ali" 3 dafa repeat ho raha hai.

Agar Ali ka name change ho jaye to 3 rows update karni parengi.

Ye redundancy hai.

---

## After Normalization

### STUDENT

| StudentID | StudentName |
|-----------|-------------|
|101|Ali|

### COURSE

| CourseID | Course |
|----------|---------|
|CS403|DBMS|
|CS304|OOP|
|CS406|AI|

### ENROLLMENT

| StudentID | CourseID |
|-----------|----------|
|101|CS403|
|101|CS304|
|101|CS406|

Ab Student Name sirf aik jagah hai.

Database zyada efficient ho gaya.

---

# Kya Normalization Compulsory Hai?

**NO**

Normalization compulsory nahi hai.

Lekin strongly recommended hai.

Normal database bhi chal sakta hai.

Lekin:

- Errors zyada hongi.
- Duplicate data hoga.
- Maintenance mushkil hogi.

Isi liye almost har professional database normalize kiya jata hai.

---

# Normalization Kis Cheez Par Depend Karti Hai?

Normalization ka base hota hai:

# Functional Dependency (FD)

Designer FD create nahi karta.

FD real world mein already hoti hai.

Designer sirf unko identify karta hai.

---

# Example

Har Student ka sirf aik Name hota hai.

```
StudentID → StudentName
```

Har Employee ki sirf aik Salary hoti hai.

```
EmployeeID → Salary
```

Ye Functional Dependency hai.

---

# Normal Forms

Database ko normalize karne ke levels ko Normal Forms kehte hain.

| Normal Form | Purpose |
|-------------|----------|
|1NF|Atomic Values|
|2NF|Remove Partial Dependency|
|3NF|Remove Transitive Dependency|
|BCNF|More Strong Version of 3NF|
|4NF|Remove Multi-Valued Dependency|
|5NF|Join Dependency|
|6NF|Very Advanced|

Practical databases mein mostly **3NF** tak hi jaya jata hai.

---

# Normalization Process

```
Requirements

↓

Logical Database Design

↓

Find Functional Dependencies

↓

Apply 1NF

↓

Apply 2NF

↓

Apply 3NF

↓

Normalized Database
```

---

# Lecture Example

Suppose ek company ka database hai.

Ek hi table banayi gayi hai.

```
WORK
(
projName,
projMgr,
empId,
hours,
empName,
budget,
startDate,
salary,
empMgr,
empDept,
rating
)
```

Is table mein:

Project bhi hai.

Employee bhi hai.

Department bhi hai.

Manager bhi hai.

Sab kuch aik hi table mein hai.

---

# Attributes Explanation

| Attribute | Meaning |
|------------|---------|
|projName|Project Name|
|projMgr|Project Manager|
|empId|Employee ID|
|hours|Employee Working Hours|
|empName|Employee Name|
|budget|Project Budget|
|startDate|Project Starting Date|
|salary|Employee Salary|
|empMgr|Employee Manager|
|empDept|Department|
|rating|Performance Rating|

---

# System Facts

Ab Designer system ko study karta hai.

Usko kuch facts milte hain.

Inhi facts se Functional Dependencies banti hain.

---

# Fact 1

Har Project ka naam unique hai.

Employee Name unique nahi.

Manager Name unique nahi.

Matlab:

Project Name identifier ban sakta hai.

Employee Name nahi.

---

# Fact 2

Har Project ka sirf aik Manager hota hai.

Isliye

```
projName → projMgr
```

---

# Example

| Project | Manager |
|----------|---------|
|Hospital System|Ahmed|
|School System|Sara|

Project pata ho.

Manager automatically mil jayega.

---

# Fact 3

Ek Project par bohot Employees kaam kar sakte hain.

Ek Employee bohot Projects par kaam kar sakta hai.

Hours depend karte hain:

Employee + Project

```
(empId, projName) → hours
```

---

# Example

| Employee | Project | Hours |
|----------|----------|-------|
|101|Hospital|20|
|101|School|12|

Employee sirf dekh kar Hours nahi milenge.

Project sirf dekh kar bhi nahi.

Dono chahiye.

---

# Fact 4

Budget aur Start Date sirf Project par depend karte hain.

```
projName → budget, startDate
```

---

# Example

| Project | Budget | Start Date |
|----------|---------|------------|
|Hospital|500000|01-Jan|
|School|200000|10-Feb|

---

# Fact 5

Employee ID unique hai.

```
empId → salary, empName
```

---

# Example

| EmployeeID | Name | Salary |
|------------|------|---------|
|101|Ali|80000|

---

# Fact 6

Employee ka apna Manager hota hai.

Project Manager se different.

```
empId → salary, empName, empMgr
```

---

# Fact 7

Har Employee aik Department mein hota hai.

Har Department ka aik Manager hota hai.

```
empDept → empMgr
```

Aur

```
empId → empDept
```

---

# Example

| Department | Manager |
|------------|----------|
|IT|Ahmed|
|HR|Sara|

---

# Fact 8

Employee ki Rating bhi Employee aur Project dono par depend karti hai.

```
(empId, projName) → rating
```

---

# Final Functional Dependencies

```
1)

empId

↓

salary
empName
empMgr
empDept
```

```
2)

(empId, projName)

↓

hours
rating
```

```
3)

projName

↓

projMgr
budget
startDate
```

```
4)

empDept

↓

empMgr
```

---

# Step 1 — First Normal Form (1NF)

Rule:

Har cell mein sirf aik value honi chahiye.

Example

❌ Wrong

| Student | Subjects |
|----------|----------|
|Ali|DBMS,OOP|

✅ Correct

| Student | Subject |
|----------|----------|
|Ali|DBMS|
|Ali|OOP|

Hamare WORK table ki values atomic hain.

Isliye

WORK already 1NF mein hai.

---

# Step 2 — Second Normal Form (2NF)

Primary Key

```
(empId, projName)
```

Problem:

Kuch columns sirf EmployeeID par depend kar rahe hain.

Kuch sirf ProjectName par.

Ye Partial Dependency hai.

---

## Solution

Table ko split kar do.

### PROJECT

| projName | projMgr | budget | startDate |
|----------|----------|---------|------------|

---

### EMPLOYEE

| empId | empName | salary | empMgr | empDept |
|--------|----------|---------|----------|----------|

---

### WORK

| empId | projName | hours | rating |
|--------|----------|-------|---------|

Ab Partial Dependency khatam.

Database 2NF mein aa gaya.

---

# Step 3 — Third Normal Form (3NF)

Ab EMPLOYEE table check karo.

```
empId

↓

empDept

↓

empMgr
```

EmployeeID directly Manager determine nahi kar raha.

Beech mein Department aa raha hai.

Ye Transitive Dependency hai.

---

# Solution

EMPLOYEE ko split karo.

---

## EMPLOYEE

| empId | empName | salary | empDept |
|--------|----------|---------|----------|

---

## DEPT

| empDept | empMgr |
|----------|---------|

Ab koi Transitive Dependency nahi.

Database 3NF mein aa gaya.

---

# Final Database

## PROJECT

| projName (PK) | projMgr | budget | startDate |
|---------------|----------|---------|------------|

---

## EMPLOYEE

| empId (PK) | empName | salary | empDept |
|------------|----------|---------|----------|

---

## WORK

| empId (FK) | projName (FK) | hours | rating |
|-------------|---------------|-------|---------|

Composite Primary Key

```
(empId, projName)
```

---

## DEPT

| empDept (PK) | empMgr |
|--------------|---------|

---

# Final Relationship Diagram

```
EMPLOYEE
   │
   │ empDept
   ▼
DEPT

EMPLOYEE
   │
   │ empId
   ▼
WORK
▲
│
│ projName
PROJECT
```

---

# Physical Database Design

Logical Design aur Normalization complete hone ke baad next phase aata hai.

# Physical Database Design

---

## Logical Design ka Focus

- Correct Database
- No Redundancy
- Consistency

---

## Physical Design ka Focus

- Speed
- Performance
- Fast Searching
- Fast Retrieval

---

# Physical Design Mein Kya Hota Hai?

Database physically kaise store hoga.

Indexes kaise banenge.

Files kaise organize hongi.

Storage kaunsi hogi.

Performance kaise improve hogi.

---

# Input Required

| Input | Purpose |
|--------|----------|
|Normalized Tables|Base Design|
|Attribute Definitions|Har field ka meaning|
|Data Usage|Kon data use karega|
|Response Time|Kitni speed chahiye|
|Security Requirements|Access control|
|Backup Requirements|Recovery|
|DBMS Tool|MySQL, Oracle, SQL Server etc.|

---

# Decisions Taken

| Decision | Example |
|-----------|---------|
|Data Type|INT, VARCHAR, DATE|
|Grouping Attributes|Related columns together|
|File Organization|Heap, Clustered|
|Indexes|Primary, Secondary|
|Access Strategy|Fast Searching|

---

# Real-Life Example

Suppose Facebook mein 50 million users hain.

Agar Index na ho.

To login slow hoga.

Agar Index use karein.

To login milliseconds mein ho jayega.

Ye Physical Database Design ka result hai.

---

# Interview Questions

### Q1. Normalization kya hai?

Database ko organize karne ka process jisme redundancy aur anomalies remove ki jati hain.

---

### Q2. Functional Dependency kya hoti hai?

Ek attribute dusre attribute ko uniquely determine kare.

Example

```
StudentID → StudentName
```

---

### Q3. 2NF kis cheez ko remove karti hai?

Partial Dependency.

---

### Q4. 3NF kis cheez ko remove karti hai?

Transitive Dependency.

---

### Q5. Physical Database Design ka objective kya hai?

Database ki performance aur execution speed improve karna.

---

# Lecture Summary

- Normalization database ko efficient aur consistent banati hai.
- Functional Dependencies normalization ki foundation hain.
- 1NF atomic values ensure karti hai.
- 2NF partial dependency remove karti hai.
- 3NF transitive dependency remove karti hai.
- Example mein WORK table ko split karke PROJECT, EMPLOYEE, WORK aur DEPT tables banaye gaye.
- Physical Database Design ka focus storage se zyada performance, indexing aur fast data access par hota hai.
