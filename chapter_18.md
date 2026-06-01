# Database Management System (CS403) – Lecture 18 Detailed Notes

# Lecture 18: Types of Joins, Relational Calculus & Introduction to Normalization

## Overview

In this lecture, we study:

- Types of Joins
- Relational Calculus
- Introduction to Normalization
- Database Anomalies

---

# 1. Joins in DBMS

A **Join** is used to combine data from two or more tables based on a related attribute.

### Why Joins are Needed?

In relational databases, data is stored in multiple tables to reduce redundancy.

Example:

### FACULTY

| facId | facName | dept |
|--------|----------|------|
| F234 | Usman | CSE |
| F236 | Ayesha | ENG |
| F237 | Samad | ENG |

### COURSE

| crCode | crTitle | fId |
|---------|----------|------|
| C3456 | Database Systems | F234 |
| C3458 | Money & Capital Market | F236 |
| C3459 | Introduction to Accounting | F237 |

If we want to know:

> Which teacher teaches which course?

We need a JOIN.

---

# Types of Joins

1. Theta Join
2. Equi Join
3. Natural Join
4. Left Outer Join
5. Right Outer Join
6. Full Outer Join
7. Semi Join

---

# 2. Theta Join

## Definition

Theta Join applies a condition before performing a cross product.

### General Form

```sql
R ⋈θ S
```

Where:

- R = First Relation
- S = Second Relation
- θ = Condition

---

## Real Example

### FACULTY

| facId | facName | rank |
|--------|----------|---------|
| F234 | Usman | Lecturer |
| F235 | Tahir | Asso Prof |
| F236 | Ayesha | Asso Prof |
| F237 | Samad | Professor |

Condition:

```sql
rank = 'Asso Prof'
```

Selected Records:

| facId | facName |
|--------|----------|
| F235 | Tahir |
| F236 | Ayesha |

Now only these records participate in the join.

### Important Point

Theta Join = Selection + Cross Product

---

# 3. Equi Join

## Definition

Equi Join combines rows having equal values in common attributes.

### Condition

```sql
FACULTY.facId = COURSE.fId
```

---

## Example

### FACULTY

| facId | facName |
|--------|----------|
| F234 | Usman |
| F236 | Ayesha |
| F237 | Samad |

### COURSE

| crCode | fId |
|---------|------|
| C3456 | F234 |
| C3458 | F236 |
| C3459 | F237 |

### Result

| facId | facName | crCode | fId |
|--------|----------|---------|------|
| F234 | Usman | C3456 | F234 |
| F236 | Ayesha | C3458 | F236 |
| F237 | Samad | C3459 | F237 |

### Key Feature

Common attributes appear twice.

Example:

```text
FACULTY.facId
COURSE.fId
```

---

# Real Life Example of Equi Join

## STUDENT

| studentId | studentName |
|------------|-------------|
| S1 | Ali |
| S2 | Ahmed |

## RESULT

| studentId | marks |
|------------|-------|
| S1 | 90 |
| S2 | 85 |

Join Condition:

```sql
STUDENT.studentId = RESULT.studentId
```

Result:

| studentName | marks |
|-------------|-------|
| Ali | 90 |
| Ahmed | 85 |

---

# 4. Natural Join

## Definition

Natural Join is similar to Equi Join.

Difference:

- Duplicate common attributes are removed.

---

## Example

### Result

| facId | facName | crCode | crTitle |
|--------|----------|---------|----------|
| F234 | Usman | C3456 | Database Systems |
| F236 | Ayesha | C3458 | Money & Capital Market |
| F237 | Samad | C3459 | Introduction to Accounting |

### Important Point

Only one copy of common attribute appears.

---

# Equi Join vs Natural Join

| Feature | Equi Join | Natural Join |
|----------|-----------|-------------|
| Common Attribute | Appears Twice | Appears Once |
| Condition | Explicitly Written | Automatically Applied |
| Output Size | Larger | Smaller |

---

# 5. Left Outer Join

## Definition

Returns:

- All records from Left Table
- Matching records from Right Table

If no match exists:

```text
NULL
```

is placed.

---

## Example

### BOOK

| bookId | title | studentId |
|---------|---------|-----------|
| B1 | DBMS | S1 |
| B2 | OS | S2 |
| B3 | Networks | NULL |

### STUDENT

| studentId | studentName |
|------------|-------------|
| S1 | Ali |
| S2 | Ahmed |

### Left Outer Join Result

| bookId | title | studentName |
|---------|---------|-------------|
| B1 | DBMS | Ali |
| B2 | OS | Ahmed |
| B3 | Networks | NULL |

### Key Feature

All rows from LEFT table remain.

---

# Real Life Example

Food Delivery App

### Orders

| orderId | customerId |
|----------|------------|
| O1 | C1 |
| O2 | C2 |
| O3 | NULL |

Even if customer information is missing:

Order O3 will still appear.

---

# 6. Right Outer Join

## Definition

Returns:

- All records from Right Table
- Matching records from Left Table

Non-matching Left records become NULL.

---

## Example

### STUDENT

| studentId | studentName |
|------------|-------------|
| S1 | Ali |
| S2 | Ahmed |
| S3 | Sara |

### BOOK

| bookId | studentId |
|---------|-----------|
| B1 | S1 |
| B2 | S2 |

### Result

| bookId | studentName |
|---------|-------------|
| B1 | Ali |
| B2 | Ahmed |
| NULL | Sara |

### Key Feature

All students appear.

---

# 7. Full Outer Join

## Definition

Combines:

```text
Left Outer Join
+
Right Outer Join
```

Returns every record from both tables.

---

## Example

### BOOK

| bookId | studentId |
|---------|-----------|
| B1 | S1 |
| B2 | S2 |
| B3 | NULL |

### STUDENT

| studentId | studentName |
|------------|-------------|
| S1 | Ali |
| S2 | Ahmed |
| S3 | Sara |

### Result

| bookId | studentName |
|---------|-------------|
| B1 | Ali |
| B2 | Ahmed |
| B3 | NULL |
| NULL | Sara |

---

# 8. Semi Join

## Definition

Steps:

1. Perform Natural Join
2. Keep attributes of first table only

---

## Example

### FACULTY

| facId | facName |
|--------|----------|
| F234 | Usman |
| F236 | Ayesha |
| F237 | Samad |

### COURSE

Contains matching records.

### Semi Join Result

| facId | facName |
|--------|----------|
| F234 | Usman |
| F236 | Ayesha |
| F237 | Samad |

Only FACULTY attributes remain.

---

# Summary of All Joins

| Join Type | Output |
|------------|---------|
| Theta Join | Selection + Cross Product |
| Equi Join | Matching Rows |
| Natural Join | Matching Rows + Remove Duplicate Columns |
| Left Join | All Left Records |
| Right Join | All Right Records |
| Full Join | All Records From Both Tables |
| Semi Join | First Table Attributes Only |

---

# 9. Relational Calculus

## Definition

Relational Calculus is a:

```text
Non-Procedural Query Language
```

User specifies:

```text
What data is needed
```

Not:

```text
How to retrieve it
```

---

# Types of Relational Calculus

1. Tuple Relational Calculus (TRC)
2. Domain Relational Calculus (DRC)

---

# 10. Tuple Relational Calculus (TRC)

## Definition

Works with entire rows (tuples).

---

## General Form

```text
{ T | P(T) }
```

Meaning:

> Find all tuples T for which predicate P(T) is true.

---

## Example

STUDENT

| studentId | credits |
|------------|---------|
| S1 | 60 |
| S2 | 45 |
| S3 | 80 |

Expression:

```text
{ S | S.credits > 50 }
```

Result:

| studentId |
|------------|
| S1 |
| S3 |

---

# Real Life Example

University wants:

> Students having more than 50 credit hours.

TRC Query:

```text
{ S | S.Credits > 50 }
```

---

# 11. Domain Relational Calculus (DRC)

## Definition

Works with individual attribute values instead of whole tuples.

---

## Example

STUDENT

| studentId | name |
|------------|------|
| S1 | Ali |
| S2 | Ahmed |

DRC:

```text
{ <id,name> | STUDENT(id,name) }
```

Result:

```text
(S1, Ali)
(S2, Ahmed)
```

---

# 12. Normalization

## Definition

Normalization is a process of organizing database tables to reduce redundancy and anomalies.

---

## Why Normalization?

Without normalization:

- Duplicate Data
- Update Problems
- Delete Problems
- Insert Problems

occur.

---

# Database Anomalies

## 1. Redundancy

Same information stored repeatedly.

### Example

| Student | Department |
|----------|------------|
| Ali | CS |
| Ahmed | CS |
| Sara | CS |

Department name repeated many times.

---

## 2. Insertion Anomaly

Unable to insert data.

### Example

Department exists but no student yet.

Cannot store department information.

---

## 3. Update Anomaly

Same data must be updated at many places.

### Example

CS renamed to Computer Science.

Need to update every record.

---

## 4. Deletion Anomaly

Deleting one record removes useful information.

### Example

Deleting last student of CS department removes department information.

---

# Normal Forms

Normalization has multiple levels.

## 1NF

First Normal Form

## 2NF

Second Normal Form

## 3NF

Third Normal Form

## BCNF

Boyce-Codd Normal Form

## 4NF

Fourth Normal Form

## 5NF

Fifth Normal Form

---

# Goal of Normalization

```text
Reduce Redundancy
+
Improve Consistency
+
Avoid Anomalies
+
Improve Maintenance
```

---

# Complete Lecture Summary

### Joins

- Theta Join
- Equi Join
- Natural Join
- Left Outer Join
- Right Outer Join
- Full Outer Join
- Semi Join

### Relational Calculus

- Tuple Relational Calculus
- Domain Relational Calculus

### Normalization

- Introduction
- Database Anomalies
- Normal Forms

### Important Exam Points

✅ Equi Join → Common column appears twice

✅ Natural Join → Common column appears once

✅ Left Join → All rows from left table

✅ Right Join → All rows from right table

✅ Full Join → All rows from both tables

✅ Semi Join → Only first table columns

✅ TRC → Works on tuples (rows)

✅ DRC → Works on domains (attribute values)

✅ Normalization removes redundancy and anomalies
