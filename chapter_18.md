# Database Management System (CS403) – Lecture 18 Detailed Notes

# Lecture 18: Types of Joins, Relational Calculus aur Introduction to Normalization

## Lecture Overview

Is lecture mein hum ye topics parhenge:

- Types of Joins
- Relational Calculus
- Normalization ka Introduction
- Database Anomalies

Pichlay lecture mein hum ne Relational Algebra ke operators parhe thay. Is lecture mein hum Joins ko detail se samjhenge jo databases mein bohat zyada use hotay hain.

---

# 1. Join Kya Hota Hai?

Join ek operation hai jo do ya zyada tables ko combine karta hai taake related data ek hi result mein hasil kiya ja sake.

## Real Life Example

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

Agar hume pata karna ho:

> Konsa teacher konsa course parha raha hai?

To hume Join use karna paray ga.

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

Theta Join mein pehle kisi table par condition lagayi jati hai phir selected records ko doosri table ke sath combine kiya jata hai.

### Formula

```text
R ⋈θ S
```

Yahan:

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

Ab sirf ye records COURSE table ke sath combine honge.

---

## Yaad Rakhein

Theta Join:

```text
Selection + Cross Product
```

---

# 3. Equi Join

## Definition

Equi Join mein do tables ki rows ko common attribute ki equal values ki bunyad par join kiya jata hai.

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

Join Condition:

```sql
FACULTY.facId = COURSE.fId
```

### Result

| facId | facName | crCode | fId |
|--------|----------|---------|------|
| F234 | Usman | C3456 | F234 |
| F236 | Ayesha | C3458 | F236 |
| F237 | Samad | C3459 | F237 |

---

## Important Point

Equi Join mein common attribute do martaba show hota hai.

Example:

```text
FACULTY.facId
COURSE.fId
```

---

# Real Life Example

### STUDENT

| studentId | studentName |
|------------|-------------|
| S1 | Ali |
| S2 | Ahmed |

### RESULT

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

Natural Join Equi Join jaisa hota hai.

Farq sirf itna hai ke duplicate common attribute ko remove kar diya jata hai.

---

## Example

### Result

| facId | facName | crCode | crTitle |
|--------|----------|---------|----------|
| F234 | Usman | C3456 | Database Systems |
| F236 | Ayesha | C3458 | Money & Capital Market |
| F237 | Samad | C3459 | Introduction to Accounting |

---

## Important Point

Natural Join mein common attribute sirf aik martaba show hota hai.

---

# Equi Join vs Natural Join

| Equi Join | Natural Join |
|------------|------------|
| Common attribute 2 dafa show hota hai | Common attribute 1 dafa show hota hai |
| Duplicate columns rehti hain | Duplicate columns remove ho jati hain |

---

# 5. Left Outer Join

## Definition

Left table ke tamam records result mein zaroor aatay hain.

Agar right table mein matching record na mile to NULL show hota hai.

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

### Result

| bookId | title | studentName |
|---------|---------|-------------|
| B1 | DBMS | Ali |
| B2 | OS | Ahmed |
| B3 | Networks | NULL |

---

## Yaad Rakhein

Left Join mein:

```text
Left Table ki tamam rows zaroor aati hain
```

---

# Real Life Example

Food Delivery App

Orders table:

| orderId | customerId |
|----------|-----------|
| O1 | C1 |
| O2 | C2 |
| O3 | NULL |

Agar customer data na bhi ho to order phir bhi result mein nazar aayega.

---

# 6. Right Outer Join

## Definition

Right table ke tamam records result mein zaroor aatay hain.

Agar left side par matching record na ho to NULL show hota hai.

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

---

## Yaad Rakhein

Right Join mein:

```text
Right Table ki tamam rows zaroor aati hain
```

---

# 7. Full Outer Join

## Definition

Full Outer Join mein dono tables ke tamam records result mein aatay hain.

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

## Formula

```text
Full Outer Join
=
Left Outer Join
+
Right Outer Join
```

---

# 8. Semi Join

## Definition

Semi Join mein:

1. Pehle Natural Join ki jati hai.
2. Phir sirf pehli table ke columns rakhe jate hain.

---

## Example

### FACULTY

| facId | facName |
|--------|----------|
| F234 | Usman |
| F236 | Ayesha |
| F237 | Samad |

### COURSE

Matching records mojood hain.

### Result

| facId | facName |
|--------|----------|
| F234 | Usman |
| F236 | Ayesha |
| F237 | Samad |

---

## Yaad Rakhein

Semi Join mein:

```text
Sirf pehli table ke attributes show hotay hain.
```

---

# Joins Ka Quick Summary

| Join Type | Result |
|------------|---------|
| Theta Join | Selection + Cross Product |
| Equi Join | Matching Records |
| Natural Join | Matching Records + Duplicate Column Remove |
| Left Join | Left Table Ki Sab Rows |
| Right Join | Right Table Ki Sab Rows |
| Full Join | Dono Tables Ki Sab Rows |
| Semi Join | Sirf First Table Ke Columns |

---

# 9. Relational Calculus

## Definition

Relational Calculus ek:

```text
Non-Procedural Query Language
```

hai.

Is mein user sirf batata hai:

```text
Kya data chahiye?
```

Ye nahi batata:

```text
Data kaise retrieve karna hai?
```

---

# Types of Relational Calculus

1. Tuple Relational Calculus (TRC)
2. Domain Relational Calculus (DRC)

---

# 10. Tuple Relational Calculus (TRC)

## Definition

TRC poori rows (tuples) par kaam karta hai.

---

## General Form

```text
{ T | P(T) }
```

Meaning:

```text
Tamam woh tuples hasil karo jin ke liye condition true ho.
```

---

## Example

### STUDENT

| studentId | credits |
|------------|---------|
| S1 | 60 |
| S2 | 45 |
| S3 | 80 |

Expression:

```text
{ S | S.Credits > 50 }
```

Result:

| studentId |
|------------|
| S1 |
| S3 |

---

## Real Life Example

University ko un students ki list chahiye jinke credits 50 se zyada hain.

Query:

```text
{ S | S.Credits > 50 }
```

---

# 11. Domain Relational Calculus (DRC)

## Definition

DRC poori row ki bajaye individual attribute values par kaam karta hai.

---

## Example

### STUDENT

| studentId | name |
|------------|------|
| S1 | Ali |
| S2 | Ahmed |

Expression:

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

Normalization database ko organize karne ka process hai.

Is ka maqsad:

- Redundancy kam karna
- Data consistency improve karna
- Database maintenance asaan banana

---

# Database Anomalies

Normalization in problems ko solve karti hai:

1. Redundancy
2. Insertion Anomaly
3. Update Anomaly
4. Deletion Anomaly

---

# 1. Redundancy

## Definition

Aik hi information ka baar baar store hona.

### Example

| Student | Department |
|----------|------------|
| Ali | CS |
| Ahmed | CS |
| Sara | CS |

Department ka naam baar baar repeat ho raha hai.

---

# 2. Insertion Anomaly

## Definition

Naya data insert karne mein problem aana.

### Example

Department exist karta hai lekin abhi us mein koi student nahi.

Department ka record insert nahi kar sakte.

---

# 3. Update Anomaly

## Definition

Aik hi data ko kai records mein update karna parna.

### Example

CS ka naam Computer Science karna hai.

Har row update karni paray gi.

---

# 4. Deletion Anomaly

## Definition

Aik record delete karne se important information bhi delete ho jana.

### Example

CS department ka aakhri student delete kar diya.

Department ki information bhi khatam ho gayi.

---

# Normal Forms

Normalization ke levels ko Normal Forms kehte hain.

- 1NF (First Normal Form)
- 2NF (Second Normal Form)
- 3NF (Third Normal Form)
- BCNF
- 4NF
- 5NF

---

# Normalization Ka Goal

```text
Redundancy Kam Karna
+
Anomalies Remove Karna
+
Consistency Improve Karna
+
Database Maintenance Asaan Banana
```

---

# Complete Lecture Summary

## Joins

- Theta Join
- Equi Join
- Natural Join
- Left Outer Join
- Right Outer Join
- Full Outer Join
- Semi Join

## Relational Calculus

- Tuple Relational Calculus (TRC)
- Domain Relational Calculus (DRC)

## Normalization

- Introduction
- Database Anomalies
- Normal Forms

## Important Exam Points

✅ Equi Join → Common column 2 dafa show hota hai

✅ Natural Join → Common column 1 dafa show hota hai

✅ Left Join → Left table ki tamam rows

✅ Right Join → Right table ki tamam rows

✅ Full Join → Dono tables ki tamam rows

✅ Semi Join → Sirf first table ke columns

✅ TRC → Rows (Tuples) par kaam karta hai

✅ DRC → Attribute values (Domains) par kaam karta hai

✅ Normalization → Redundancy aur anomalies ko remove karti hai
