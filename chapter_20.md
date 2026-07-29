# 📚 CS403 – Database Management Systems
# Lecture 20 – Second Normal Form (2NF), Third Normal Form (3NF), BCNF & Higher Normal Forms
---

# 🎯 Learning Objectives

Is lecture ke baad aap ko ye concepts achi tarah samajh aa jayenge.

- ✅ Second Normal Form (2NF)
- ✅ Partial Dependency
- ✅ Third Normal Form (3NF)
- ✅ Transitive Dependency
- ✅ Boyce-Codd Normal Form (BCNF)
- ✅ Higher Normal Forms (4NF, 5NF)
- ✅ Har Normal Form ki Problems
- ✅ Har Normal Form ke Examples
- ✅ Exam Tips

---

# Pehle Revision

Database Normalization ka purpose kya hai?

Simple words mein

> Database ko clean banana.

Yani

- Duplicate Data remove karna
- Storage kam use karna
- Database ko fast banana
- Errors remove karna
- Data ko organize karna

---

# Ab tak hum kya parh chuke hain?

## UNF

Data messy hota hai.

Example

| Student | Courses |
|----------|---------|
| Ali | OOP, DBMS |

Ek cell mein multiple values.

---

## 1NF

Rule

✅ Har cell mein sirf ek value hogi.

Example

| Student | Course |
|----------|---------|
| Ali | OOP |
| Ali | DBMS |

Ab table 1NF mein hai.

Lekin abhi bhi kuch problems hain.

Isi liye 2NF ki zarurat parti hai.

---

# Second Normal Form (2NF)

## Definition

A relation tab 2NF mein hota hai jab

- Wo pehle se 1NF mein ho.
- Har Non-Key Attribute Primary Key par **Fully Dependent** ho.

---

# Sab se Important Question

## Fully Dependent kya hota hai?

Agar Primary Key Composite hai

Example

```
(StudentID, CourseID)
```

Aur Student Name sirf StudentID se mil raha hai

```
StudentID → StudentName
```

To ye Full Dependency nahi hai.

Ye **Partial Dependency** hai.

---

# Partial Dependency

## Definition

Jab Composite Primary Key ka sirf ek part kisi attribute ko determine kare to usay Partial Dependency kehte hain.

Diagram

```
(StudentID, CourseID)
      |
      |
StudentID --------> StudentName
```

Student Name ko CourseID ki zarurat hi nahi.

Isliye ye Partial Dependency hai.

---

# Example 1

## CLASS Table

| CourseID | StudentID | StudentName | Faculty | Room | Grade |
|-----------|-----------|-------------|----------|------|-------|
| C101 | S01 | Ali | F01 | 101 | A |
| C102 | S01 | Ali | F02 | 202 | B |
| C101 | S02 | Ahmed | F01 | 101 | A |
| C102 | S03 | Sara | F02 | 202 | B |

---

Primary Key

```
(CourseID, StudentID)
```

Functional Dependencies

```
(CourseID, StudentID)
        ↓
StudentName
Faculty
Room
Grade

StudentID → StudentName

CourseID → Faculty
CourseID → Room
```

---

# Problem Kahan Hai?

Student Name sirf StudentID par depend kar raha hai.

Faculty sirf CourseID par depend kar rahi hai.

Room sirf CourseID par depend kar raha hai.

Ye sab Partial Dependencies hain.

Matlab

❌ Table 2NF mein nahi hai.

---

# Visual Understanding

```
Primary Key

(CourseID, StudentID)

      |
      |

CourseID --------> Faculty

CourseID --------> Room

StudentID -------> StudentName
```

Ye sari Partial Dependencies hain.

---

# Is Table Mein Konsi Problems Hain?

## 1. Redundancy

Faculty repeat ho rahi hai.

| Course | Faculty |
|---------|----------|
| C101 | F01 |
| C101 | F01 |

Same data baar baar.

---

## 2. Insertion Anomaly

Naya Course create hua.

Lekin koi student register nahi hua.

Hum insert nahi kar sakte.

---

## 3. Deletion Anomaly

Ek course mein sirf ek student tha.

Us student ka record delete kiya.

Course bhi delete ho gaya.

---

## 4. Update Anomaly

Room 101 ko 105 karna hai.

Agar 100 students enrolled hain.

To 100 rows update karni hongi.

Ek row miss ho gayi to database inconsistent ho jayega.

---

# 2NF Ka Solution

Table ko tod do.

---

## STUDENT Table

| StudentID | StudentName |
|------------|-------------|
| S01 | Ali |
| S02 | Ahmed |
| S03 | Sara |

---

## COURSE Table

| CourseID | Faculty | Room |
|-----------|----------|------|
| C101 | F01 |101|
| C102 |F02|202|

---

## CLASS Table

| CourseID | StudentID | Grade |
|-----------|-----------|-------|
| C101 |S01|A|
| C102 |S01|B|
| C101 |S02|A|
| C102 |S03|B|

---

# Ab Fayda Kya Hua?

✅ Duplicate Data remove

✅ Update easy

✅ Insert easy

✅ Delete safe

---

# 2NF Yaad Karne ki Trick

```
2NF

↓

Remove

Partial Dependency
```

Bas.

Ye exam ka favourite point hai.

---

# Third Normal Form (3NF)

Ab maan lo table already 2NF mein hai.

Phir bhi problem ho sakti hai.

Wo problem hai

## Transitive Dependency

---

# Definition

Jab

Primary Key

↓

Non-Key Attribute

↓

Dusra Non-Key Attribute

To isay kehte hain

Transitive Dependency

---

# Example

## STUDENT

| StudentID | Name | Address | Program | Credits |
|------------|------|----------|----------|----------|
|S01|Ali|Karachi|BSCS|132|
|S02|Ahmed|Lahore|BSSE|135|
|S03|Sara|Islamabad|BSCS|132|

---

Primary Key

```
StudentID
```

Functional Dependencies

```
StudentID

↓

Program

↓

Credits
```

Program Credits StudentID se directly nahi aa rahe.

Program se aa rahe hain.

Ye Transitive Dependency hai.

---

# Visual Diagram

```
StudentID

↓

Program

↓

Credits
```

Credits indirectly StudentID se mil rahe hain.

---

# Problem

Har BSCS Student ke sath

132

baar baar repeat ho raha hai.

---

# Agar BSCS Credits Change Ho Jaye?

132

↓

136

Ab jitne students BSCS mein hain

Sab update karne honge.

---

# Solution

Program ko separate table bana do.

---

## STUDENT

| StudentID | Name | Address | Program |
|------------|------|----------|----------|
|S01|Ali|Karachi|BSCS|
|S02|Ahmed|Lahore|BSSE|
|S03|Sara|Islamabad|BSCS|

---

## PROGRAM

| Program | Credits |
|----------|----------|
|BSCS|132|
|BSSE|135|

---

# Ab Fayda

Credits sirf ek jagah hain.

Duplicate nahi.

---

# 3NF Yaad Karne ki Trick

```
3NF

↓

Remove

Transitive Dependency
```

---

# Difference Between 2NF and 3NF

| 2NF | 3NF |
|------|------|
| 1NF hona zaruri | 2NF hona zaruri |
| Partial Dependency remove | Transitive Dependency remove |
| Composite Key par focus | Non-Key Attributes par focus |
| Fully Dependent hona chahiye | Non-Key kisi Non-Key par depend nahi karega |

---

# BCNF (Boyce-Codd Normal Form)

Ye 3NF ka advanced version hai.

Rule

> Har Determinant Candidate Key hona chahiye.

Simple language

Jo attribute kisi aur attribute ko determine kare

Wo Candidate Key hona chahiye.

---

# BCNF Example

## ENROLL

| StudentNo | StudentName | CourseNo | CourseName | Date |
|------------|-------------|----------|-------------|------|
|101|Ali|CS101|DBMS|10-Jan|
|102|Ahmed|CS101|DBMS|11-Jan|

Dependencies

```
StudentNo → StudentName

CourseNo → CourseName
```

Problem

Student Name repeat.

Course Name repeat.

---

# BCNF Solution

## STUDENT

| StudentNo | StudentName |
|------------|-------------|
|101|Ali|
|102|Ahmed|

---

## COURSE

| CourseNo | CourseName |
|-----------|------------|
|CS101|DBMS|

---

## ENROLLMENT

| StudentNo | CourseNo | Date |
|------------|----------|------|
|101|CS101|10-Jan|
|102|CS101|11-Jan|

---

# BCNF Yaad Karne ki Trick

```
Every Determinant

Must Be

Candidate Key
```

---

# Higher Normal Forms

## 4NF

Deals with

Multi-Valued Dependency

Example

Ek teacher multiple subjects aur multiple languages janta hai.

Ye alag issue hai.

---

## 5NF

Deals with

Lossless Join

Database ko todne ke baad dubara join karne se data loss nahi hona chahiye.

---

## DKNF

Domain Key Normal Form

Sab se advanced.

Real-life mein bohat kam use hoti hai.

---

# Comparison Table

| Normal Form | Kis Problem ko Remove Karti Hai |
|--------------|--------------------------------|
| 1NF | Repeating Groups |
| 2NF | Partial Dependency |
| 3NF | Transitive Dependency |
| BCNF | Every Determinant Candidate Key |
| 4NF | Multi-Valued Dependency |
| 5NF | Join Dependency |

---

# Complete Flow

```
UNF

↓

1NF

↓

2NF

↓

3NF

↓

BCNF

↓

4NF

↓

5NF
```

---

# Real-Life Example

Imagine School Database

## Poor Design

| Student | Course | Teacher | Room |
|----------|---------|----------|------|
|Ali|DBMS|Sir A|101|
|Ahmed|DBMS|Sir A|101|
|Sara|DBMS|Sir A|101|

Teacher aur Room baar baar repeat.

---

## Better Design (2NF)

### STUDENT

| StudentID | Name |
|------------|------|
|S01|Ali|
|S02|Ahmed|
|S03|Sara|

### COURSE

| CourseID | Teacher | Room |
|-----------|----------|------|
|C01|Sir A|101|

### ENROLLMENT

| StudentID | CourseID |
|------------|-----------|
|S01|C01|
|S02|C01|
|S03|C01|

---

# Exam Important Definitions

## 2NF

A relation is in Second Normal Form if it is in 1NF and every non-key attribute is fully functionally dependent on the whole primary key.

---

## 3NF

A relation is in Third Normal Form if it is already in 2NF and no non-key attribute depends on another non-key attribute.

---

## BCNF

A relation is in BCNF if every determinant is a candidate key.

---

# Memory Tricks

## 2NF

```
P

↓

Partial

↓

Remove
```

---

## 3NF

```
T

↓

Transitive

↓

Remove
```

---

## BCNF

```
Every

Determinant

=

Candidate Key
```

---

# One-Line Revision

- **1NF** → Har cell mein sirf ek value.
- **2NF** → Partial Dependency remove.
- **3NF** → Transitive Dependency remove.
- **BCNF** → Har Determinant Candidate Key.
- **4NF** → Multi-Valued Dependency remove.
- **5NF** → Join Dependency remove.

---

# Final Exam Tips ⭐

### Yaad rakhne wali sab se important baatein:

- 2NF sirf **Composite Primary Key** ke case mein issue ban sakta hai.
- Partial Dependency sirf 2NF ka topic hai.
- Transitive Dependency sirf 3NF ka topic hai.
- BCNF, 3NF se zyada strict hota hai.
- Har Normal Form ka main goal **Redundancy aur Anomalies ko remove karna** hai.

---

# Short Revision Table

| Topic | Remember |
|--------|----------|
| 1NF | Atomic Values |
| 2NF | Fully Dependent |
| Partial Dependency | Composite Key ka ek part determine kare |
| 3NF | No Transitive Dependency |
| Transitive Dependency | Non-Key → Non-Key |
| BCNF | Determinant = Candidate Key |
| Goal of Normalization | Clean, Consistent & Efficient Database |

---

# 🎉 Congratulations!

Agar aap ne ye notes achi tarah samajh liye hain, to aap **2NF, 3NF aur BCNF** ke concepts ko exam mein asani se explain kar sakte hain aur in se related numericals/examples bhi solve kar sakte hain.
