# Database Management System (CS403) - Lecture 17 Notes

# Relational Algebra (Part 2)

## Overview

Is lecture mein hum ne Relational Algebra ke Binary Operators ko detail mein study kiya:

1. Union (U)
2. Intersection (∩)
3. Set Difference (-)
4. Cartesian Product (X)
5. Join Operation (Introduction)

Relational Algebra ek procedural query language hai jo relations (tables) par operations perform karti hai aur result mein nayi relation (table) produce karti hai.

---

# 1. Union Operation (U)

## Definition

Union operation do tables ke records ko combine karti hai.

Result mein woh tamam tuples (rows) aati hain jo:

- Pehli table mein hon
- Ya doosri table mein hon
- Ya dono mein hon

Duplicate rows automatically remove ho jati hain.

---

## Union Compatible Relations

Union operation lagane ke liye dono tables ka Union Compatible hona zaroori hai.

### Condition 1: Same Degree

Dono tables mein columns ki quantity same honi chahiye.

### Example

### Table A

| StudentID | Name |
|------------|------|
| S1 | Ali |
| S2 | Ahmed |

### Table B

| StudentID | Name |
|------------|------|
| S3 | Sara |
| S4 | Fatima |

Dono tables mein 2 columns hain.

✓ Union Compatible

---

## Condition 2: Same Domain

Corresponding columns ka data type aur meaning same hona chahiye.

### Correct

| StudentID | Name |

| StudentID | Name |

✓ Compatible

### Incorrect

| StudentID | Name |

| CourseID | CreditHours |

✗ Not Compatible

---

## Symbol

```text
R U S
```

---

## Commutative Property

```text
R U S = S U R
```

Order change karne se result same rehta hai.

---

## Real Example

### COURSE1

| CourseID | CourseTitle |
|-----------|------------|
| C101 | DBMS |
| C102 | OOP |
| C103 | Networking |

### COURSE2

| CourseID | CourseTitle |
|-----------|------------|
| C103 | Networking |
| C104 | AI |

### Query

```text
COURSE1 U COURSE2
```

### Output

| CourseID | CourseTitle |
|-----------|------------|
| C101 | DBMS |
| C102 | OOP |
| C103 | Networking |
| C104 | AI |

Networking duplicate tha is liye sirf ek dafa show hua.

---

## Real-Life Scenario

Karachi campus aur Lahore campus ke offered courses ko combine karna:

```text
KarachiCourses U LahoreCourses
```

Result:

Tamam unique courses ki list.

---

# 2. Intersection Operation (∩)

## Definition

Intersection operation sirf woh tuples return karti hai jo dono tables mein common hon.

---

## Requirements

Intersection ke liye bhi Union Compatibility zaroori hai.

- Same degree
- Same domains

---

## Symbol

```text
R ∩ S
```

---

## Commutative Property

```text
R ∩ S = S ∩ R
```

---

## Example

### COURSE1

| CourseID | CourseTitle |
|-----------|------------|
| C101 | DBMS |
| C102 | OOP |
| C103 | Networking |

### COURSE2

| CourseID | CourseTitle |
|-----------|------------|
| C103 | Networking |
| C104 | AI |

### Query

```text
COURSE1 ∩ COURSE2
```

### Output

| CourseID | CourseTitle |
|-----------|------------|
| C103 | Networking |

Sirf common course show hua.

---

## Real-Life Scenario

Do departments ke common employees find karna:

```text
DepartmentA ∩ DepartmentB
```

Result:

Sirf common employees.

---

# 3. Set Difference Operation (-)

## Definition

Difference operation un tuples ko return karti hai jo pehli relation mein hon lekin doosri relation mein na hon.

---

## Symbol

```text
R - S
```

---

## Example

### COURSE1

| CourseID | CourseTitle |
|-----------|------------|
| C101 | DBMS |
| C102 | OOP |
| C103 | Networking |

### COURSE2

| CourseID | CourseTitle |
|-----------|------------|
| C103 | Networking |
| C104 | AI |

### Query

```text
COURSE1 - COURSE2
```

### Output

| CourseID | CourseTitle |
|-----------|------------|
| C101 | DBMS |
| C102 | OOP |

Networking remove ho gaya kyun ke wo COURSE2 mein bhi tha.

---

## Real-Life Scenario

Students jin ki registration ho chuki hai lekin fee submit nahi hui:

```text
RegisteredStudents - FeePaidStudents
```

Result:

Fee na dene wale students.

---

# Difference vs Intersection

| Operation | Result |
|------------|---------|
| Intersection | Common records |
| Difference | Unique records of first table |

---

# 4. Cartesian Product (X)

## Definition

Cartesian Product har row ko doosri table ki har row ke sath combine karta hai.

Is ko Cross Product bhi kehte hain.

---

## Symbol

```text
R X S
```

---

## Important Point

Cartesian Product ke liye Union Compatibility ki zaroorat nahi hoti.

Tables:

- Different columns rakh sakti hain
- Different data types rakh sakti hain

---

## Formula

Agar:

R mein = C rows

S mein = D rows

To:

```text
Rows = C × D
```

---

Agar:

R mein = m columns

S mein = n columns

To:

```text
Columns = m + n
```

---

## Example

### COURSE

| CourseID | CourseTitle |
|-----------|------------|
| C101 | DBMS |
| C102 | OOP |
| C103 | AI |

### STUDENT

| StudentID | Name |
|-----------|------|
| S1 | Ali |
| S2 | Ahmed |

---

### Query

```text
COURSE X STUDENT
```

---

### Output

| CourseID | CourseTitle | StudentID | Name |
|-----------|------------|-----------|------|
| C101 | DBMS | S1 | Ali |
| C102 | OOP | S1 | Ali |
| C103 | AI | S1 | Ali |
| C101 | DBMS | S2 | Ahmed |
| C102 | OOP | S2 | Ahmed |
| C103 | AI | S2 | Ahmed |

---

### Calculation

Courses = 3

Students = 2

```text
3 × 2 = 6 Rows
```

---

## Real-Life Scenario

Company ke tamam employees ko tamam projects ke sath pair karna:

```text
EMPLOYEE X PROJECT
```

Har employee har project ke sath combine hoga.

---

# Cartesian Product Properties

## Commutative

```text
R X S = S X R
```

## Associative

```text
(R X S) X T = R X (S X T)
```

---

# 5. Join Operation

## Definition

Join operation Cartesian Product ka special form hai.

Join sirf matching records ko combine karti hai.

---

## Why Join is Needed?

Database mein data aksar multiple tables mein store hota hai.

Join tables ke darmiyan relationship establish karti hai.

---

# Example

## STUDENT

| StudentID | StudentName |
|------------|------------|
| S1 | Ali |
| S2 | Ahmed |

---

## BOOK

| BookID | StudentID | BookName |
|---------|-----------|----------|
| B1 | S1 | DBMS |
| B2 | S1 | OOP |
| B3 | S2 | Java |

---

## Join Query

```text
STUDENT JOIN BOOK
ON STUDENT.StudentID = BOOK.StudentID
```

---

## Output

| StudentName | BookName |
|------------|----------|
| Ali | DBMS |
| Ali | OOP |
| Ahmed | Java |

---

## Explanation

StudentID dono tables mein common attribute hai.

Isi attribute ki basis par join perform hua.

---

# Primary Key and Foreign Key in Join

## STUDENT Table

```text
StudentID (Primary Key)
```

Unique value.

---

## BOOK Table

```text
StudentID (Foreign Key)
```

Reference to STUDENT table.

---

## Relationship

```text
STUDENT.StudentID
=
BOOK.StudentID
```

Isi relation par join hota hai.

---

# Real-Life Example

University chahti hai:

"Har student ki issued books ki list dikhao"

To:

```text
STUDENT JOIN BOOK
```

Use kiya jayega.

---

# Summary Table

| Operator | Symbol | Purpose |
|-----------|---------|----------|
| Select | σ | Rows filter karta hai |
| Project | π | Columns select karta hai |
| Union | U | Dono tables ke unique records combine karta hai |
| Intersection | ∩ | Common records return karta hai |
| Difference | - | Pehli table ke unique records return karta hai |
| Cartesian Product | X | Har row ko har row ke sath combine karta hai |
| Join | ⋈ | Matching records ko combine karta hai |

---

# Exam Important Points

### Union

- Same degree required
- Same domains required
- Duplicate tuples remove hoti hain

### Intersection

- Sirf common tuples return karta hai
- Union compatible relations required

### Difference

- First relation ke unique tuples return karta hai

### Cartesian Product

- Union compatibility required nahi
- Rows = R rows × S rows
- Columns = R columns + S columns

### Join

- Cartesian Product ka special form
- Matching records ko combine karta hai
- Primary Key aur Foreign Key ke zariye perform hota hai

---

# One-Line Revision

- Union → Combine unique records
- Intersection → Find common records
- Difference → Find missing records
- Cartesian Product → All possible combinations
- Join → Combine related records
