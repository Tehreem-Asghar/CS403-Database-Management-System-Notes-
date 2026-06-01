# Lecture 14 - Logical Database Design & Relational Data Model (RDM)

# Introduction

Is lecture mein hum **Logical Database Design** aur **Relational Data Model (RDM)** ke concepts ko detail mein samjhein ge.

Database development process mein pehle **Conceptual Database Design** banti hai (E-R Diagram ki form mein), phir usay **Logical Database Design** mein convert kiya jata hai.

Aaj ke zamane mein Logical Database Design ke liye sab se zyada use hone wala model:

**Relational Data Model (RDM)**

hai.

---

# Conceptual Database Design vs Logical Database Design

| Conceptual Database Design | Logical Database Design |
|---------------------------|-------------------------|
| E-R Model mein develop hoti hai | Relational Model mein develop hoti hai |
| Analysis phase ka result hoti hai | Conceptual design ko convert karke banayi jati hai |
| Graphical hoti hai | Descriptive hoti hai |
| Zyada expressive hoti hai | Comparatively kam expressive hoti hai |
| Direct implement nahi hoti | Direct implement hoti hai |
| Data model independent hoti hai | DBMS independent hoti hai |

---

# Data Model Kya Hota Hai?

Data Model tools aur rules ka collection hota hai jo database design karne ke liye use kiya jata hai.

Har Data Model ke 3 major components hote hain:

1. Construct
2. Manipulation Language
3. Integrity Constraints

---

# Relational Data Model (RDM)

Relational Data Model ko 1970 mein IBM ke scientist **E.F. Codd** ne introduce kiya tha.

Aaj ke lagbhag tamam databases isi model par based hain.

Examples:

- Oracle
- SQL Server
- MySQL
- PostgreSQL
- DB2

---

# RDM Ki Popularity Ke Reasons

## 1. Simplicity

RDM mein sirf aik structure use hota hai:

**Relation (Table)**

Table ko samajhna aur use karna bohat asaan hota hai.

### Example

| StudentID | StudentName |
|------------|-------------|
| S001 | Ali |
| S002 | Ahmed |

---

## 2. Strong Mathematical Foundation

RDM mathematics par based hai.

Is wajah se:

- Har cheez precisely define hoti hai.
- Ambiguity nahi hoti.
- Rules mathematically verify kiye ja sakte hain.
- Query languages mathematically derived hain.

---

# Relational Data Model Ka Basic Structure

RDM ka basic structure:

## Relation

Relation ko database mein table ki form mein represent kiya jata hai.

---

# Table

Table rows aur columns par mushtamil hoti hai.

Example:

| stID | stName | Class | DOB | Gender |
|------|---------|--------|---------|---------|
| S001 | Ali | MCS | 12/06/2000 | M |
| S002 | Ahmed | BCS | 15/08/2001 | M |
| S003 | Sana | MBA | 20/02/2000 | F |

---

# Important Terminology

## Row

Row ko Tuple ya Record bhi kehte hain.

Example:

| S001 | Ali | MCS | 12/06/2000 | M |

Yeh aik row hai.

---

## Column

Column ko Attribute bhi kehte hain.

Example:

```text
stID
stName
Class
DOB
Gender
```

Yeh sab attributes hain.

---

# Basic Properties of Database Relations

Database relation ki 6 important properties hoti hain.

---

# 1. Har Cell Mein Atomic Value Hogi

Atomic ka matlab:

**Single Value**

Har cell mein sirf aik value store hogi.

---

## Correct Example

| StudentName |
|-------------|
| Ali |

---

## Wrong Example

| StudentName |
|-------------|
| Ali, Ahmed, Sana |

Yahan multiple values hain jo allowed nahi hain.

---

## Real Life Example

Agar student ki hobbies:

```text
Cricket
Football
Reading
```

hain to in sab ko aik hi cell mein store nahi karna chahiye.

Alag table banayi jati hai.

---

# 2. Har Column Ka Unique Name Hoga

Do columns ka naam same nahi ho sakta.

---

## Correct Example

| StudentID | StudentName |

---

## Wrong Example

| StudentName | StudentName |

Duplicate column names allowed nahi.

---

# 3. Attribute Values Same Domain Se Aayengi

Domain ka matlab:

**Allowed Values Ka Set**

---

## Example

Attribute:

```text
DOB
```

Domain:

```text
Date
```

---

### Correct Values

```text
12/05/2000

10/08/2001
```

---

### Wrong Values

```text
Ali

5000
```

Kyun ke DOB sirf Date accept karega.

---

## Real Life Example

Gender attribute ka domain:

```text
M
F
```

Is field mein sirf M ya F enter ho sakta hai.

---

# 4. Columns Ka Order Important Nahi

Columns ki position change karne se relation change nahi hota.

---

## Table 1

| ID | Name | Age |

---

## Table 2

| Age | Name | ID |

Dono same relation represent karte hain.

---

# 5. Rows Ka Order Important Nahi

Rows ko upar neeche kar dene se relation same rehta hai.

---

## Example

### Table A

| Name |
|--------|
| Ali |
| Ahmed |
| Sana |

### Table B

| Name |
|--------|
| Sana |
| Ali |
| Ahmed |

Dono same relation hain.

---

# 6. Har Row Unique Hogi

Do rows bilkul same nahi ho sakti.

---

## Wrong Example

| ID | Name |
|-----|------|
| S001 | Ali |
| S001 | Ali |

---

## Correct Example

| ID | Name |
|-----|------|
| S001 | Ali |
| S002 | Ali |

ID different hai.

---

# Mathematical Relations

Relational Data Model mathematics ke relation concept par based hai.

---

# Set

Set values ka collection hota hai.

Example:

```text
A = {x, y}

B = {2, 4, 6}
```

---

# Cartesian Product

Cartesian Product har possible combination generate karta hai.

Formula:

```text
A × B
```

Result:

```text
A × B = {

(x,2)

(x,4)

(x,6)

(y,2)

(y,4)

(y,6)

}
```

---

# Relation

Cartesian Product ka koi bhi subset relation kehlata hai.

Example:

```text
R1 = {

(x,2)

(y,2)

(x,6)

(x,4)

}
```

Yeh Relation hai kyun ke yeh Cartesian Product ka subset hai.

---

# Real World Example

## Name Set

```text
Name = {

Ali

Sana

Ahmed

Sara

}
```

## Age Set

```text
Age = {

15

16

17

18

...

25

}
```

---

# Cartesian Product

```text
Name × Age
```

Is mein tamam possible combinations hongi.

Example:

```text
(Ali,15)

(Ali,16)

(Ali,17)

...

(Sara,25)
```

---

# CLASS Relation

Agar hum subset select karein:

```text
CLASS = {

(Ali,18)

(Sana,17)

(Ahmed,19)

(Ali,20)

}
```

To yeh aik mathematical relation hai.

---

# Database Context Mein Relation

Database mein:

```text
(Ali,18)
```

Aik tuple hai.

Yahan:

```text
Ali = Name Attribute Value

18 = Age Attribute Value
```

---

# Relation Schema

Relation Schema attributes aur domains define karti hai.

General Form:

```text
R = (

A1:D1,

A2:D2,

A3:D3,

...

An:Dn

)
```

---

# Student Schema Example

```text
STD = (

stID : Text,

stName : Text,

stAddress : Text,

DOB : Date

)
```

Short Form:

```text
STD(

stID,

stName,

stAddress,

DOB

)
```

---

# Domain Explanation

| Attribute | Domain |
|------------|---------|
| stID | Text |
| stName | Text |
| stAddress | Text |
| DOB | Date |

---

# Database Relation Example

```text
STD = {

(S001, Ali, Lahore, 12/12/2000),

(S002, Ahmed, Karachi, 15/05/2001)

}
```

---

# Table Representation

| stID | stName | stAddress | DOB |
|-------|---------|-----------|---------|
| S001 | Ali | Lahore | 12/12/2000 |
| S002 | Ahmed | Karachi | 15/05/2001 |

---

# Relation Schema vs Relation

## Relation Schema

Structure define karti hai.

Example:

```text
STD(

stID,

stName,

stAddress,

DOB

)
```

---

## Relation

Actual records ko represent karti hai.

Example:

```text
(S001, Ali, Lahore, 12/12/2000)

(S002, Ahmed, Karachi, 15/05/2001)
```

---

# Real-Life Student Database Example

## Schema

```text
STUDENT(

StudentID,

StudentName,

Gender,

Age,

City
)
```

---

## Records

| StudentID | StudentName | Gender | Age | City |
|------------|------------|---------|------|------|
| S001 | Ali | M | 20 | Karachi |
| S002 | Sana | F | 21 | Lahore |
| S003 | Ahmed | M | 19 | Islamabad |

---

# Components of Relational Data Model

## 1. Construct

Relation (Table)

---

## 2. Manipulation Language

SQL

Example:

```sql
SELECT * FROM STUDENT;
```

---

## 3. Integrity Constraints

Data correctness ensure karte hain.

Examples:

- Primary Key
- Foreign Key
- Unique Constraint
- Not Null Constraint

---

# Key Points For Exam

1. Relational Data Model ko E.F. Codd ne 1970 mein introduce kiya.
2. RDM ki strength:
   - Simplicity
   - Strong Mathematical Foundation
3. Relation ko table ki form mein represent kiya jata hai.
4. Row = Tuple = Record
5. Column = Attribute
6. Relation Cartesian Product ka subset hoti hai.
7. Har cell atomic value rakhti hai.
8. Column names unique hote hain.
9. Rows aur columns ka order matter nahi karta.
10. Har row unique hoti hai.
11. Relation Schema structure define karti hai.
12. Relation actual data store karti hai.

# Short Summary

Logical Database Design conceptual design ko relational form mein convert karti hai. Relational Data Model tables par based hota hai aur mathematics ke relation concept se derive kiya gaya hai. Database relation ko table ki form mein represent kiya jata hai jahan rows records ko aur columns attributes ko represent karte hain. Har relation Cartesian Product ka subset hota hai aur us ki kuch important properties hoti hain jaise atomic values, unique columns aur unique rows.
