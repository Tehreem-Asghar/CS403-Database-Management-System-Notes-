# 📘 Database Management System (CS403) — Lecture 02 Detailed Notes

# Introduction

Is lecture me humne Database Systems ke advantages, costs, data ki importance, data ke levels aur database users ke bare me detail me study kiya.

---

# Difference Between Data and Information

## Data

Data raw facts ka collection hota hai jo kisi specific purpose ke liye collect kiya jata hai.

### Example:
- Ali
- 21
- BSCS

Ye sirf raw values hain, inse hume proper meaning samajh nahi aata.

---

## Information

Jab data ko process karke meaningful form me convert kiya jata hai to usay Information kehte hain.

### Example:

| Name | Age | Class |
|---|---|---|
| Ali | 21 | BSCS |

Ab data meaningful ban gaya kyunki labels attach kar diye gaye hain.

---

# Schema

Schema database ka structure hota hai jo define karta hai ke data kis format me store hoga.

Schema ko database ka blueprint bhi kaha jata hai.

---

## Schema batata hai:

- Data kis type ka hoga
- Data ka size kya hoga
- Attributes kitne honge
- Data kis tarah organize hoga

---

## Real Life Example

Agar school database banana ho to schema kuch is tarah ho sakta hai:

| Field Name | Data Type | Size |
|---|---|---|
| StudentName | Character | 30 |
| Age | Integer | 4 Bytes |
| Class | Character | 10 |

---

# Database Application

Database Application wo software hota hai jo database par operations perform karta hai.

---

## Operations

- Insert Data
- Update Data
- Delete Data
- Retrieve Data

---

## Real Life Example

### School Management System

Aik school software:

- Student admission karta hai
- Attendance save karta hai
- Result generate karta hai

Ye sab database applications hain.

---

# Database Management System (DBMS)

DBMS programs ka collection hota hai jo database ko manage karta hai.

---

# Main Functions of DBMS

## 1. Data Management

DBMS decide karta hai:

- Data kaise store hoga
- Data kaise retrieve hoga
- Data kaise organize hoga

---

## 2. User Management

DBMS users ko manage karta hai aur permissions control karta hai.

---

## Example

### Bank System

- Customer sirf apna account dekh sakta hai
- Manager sab accounts dekh sakta hai

Ye control DBMS karta hai.

---

# Advantages of Database Systems

# 1. Data Consistency

Consistency ka matlab hai ke har jagah same data available ho.

---

## Example

Agar student ka naam:

- Admission section me "Ali"
- Examination section me bhi "Ali"

to data consistent hai.

Agar aik jagah "Ali" aur dusri jagah "Aly" ho to inconsistency hogi.

---

# 2. Better Data Security

DBMS data ko unauthorized access se protect karta hai.

---

## Example

University portal me:

- Student sirf apna result dekh sakta hai
- Teacher sab students ke marks update kar sakta hai

---

# 3. Faster Application Development

Database pehle se available hota hai is liye new applications banana easy hota hai.

---

## Example

Agar school database already bana hua hai to usi database se:

- Attendance System
- Fee System
- Examination System

asani se ban sakte hain.

---

# 4. Economy of Scale

Aik hi data multiple departments use kar sakte hain.

---

## Example

Admission department ka student data:

- Attendance department
- Examination department
- Library department

sab use kar sakte hain.

---

# 5. Better Concurrency Control

Multiple users aik hi time par database access kar sakte hain.

---

## Example

ATM System

Duniya bhar ke ATM machines aik central database se connected hoti hain aur hazaron users aik hi waqt me transactions perform karte hain.

DBMS ensure karta hai ke sab operations correctly perform hon.

---

# 6. Better Backup and Recovery

DBMS backup aur recovery facilities provide karta hai.

---

## Example

Agar hard disk crash ho jaye to backup se data restore kiya ja sakta hai.

---

# Costs Involved in Database Systems

# 1. High Cost

Database systems expensive hote hain.

---

## Expenses

- Specialized Software
- Hardware
- Technical Staff

---

## Example

Large bank ko powerful servers aur professional DBAs hire karne padte hain.

---

# 2. Conversion Cost

Old system ko database system me convert karna costly hota hai.

---

## Example

Agar kisi company ka manual record system ho to usay computerized database me convert karna time aur money leta hai.

---

# 3. Difficult Recovery Procedures

Database recovery technical process hota hai.

---

## Example

Agar database corrupt ho jaye to usay recover karne ke liye skilled DBA ki zarurat hoti hai.

---

# Importance of Data

Data organization ka bohat important resource hota hai.

---

# Why Data is Important?

Organizations correct decisions lene ke liye data use karti hain.

Agar correct data available na ho to wrong decisions liye ja sakte hain.

---

## Real Life Example

Agar hospital ke paas patient ka correct medical record na ho to treatment me problem ho sakti hai.

---

# Levels of Data

# 1. Real World Data

Ye wo level hai jahan entities reality me exist karti hain.

---

## Example

Student

Attributes:

- Name
- Roll Number
- Class
- Age

---

# 2. Meta Data

Meta Data data ke bare me information hoti hai.

---

## Example

| Field | Type | Size |
|---|---|---|
| Name | Character | 25 |
| Age | Integer | 4 |
| Class | Character | 10 |

---

# 3. Existence of Data

Actual stored values ko existence of data kehte hain.

---

## Example

| Name | Age | Class |
|---|---|---|
| Ali | 21 | BSCS |
| Ahmed | 22 | BBA |

---

# Users of Database Systems

# 1. Application Programmers

Ye wo log hote hain jo database applications banate hain.

---

## Example

Software Developers

Jo:

- School Management System
- Banking System
- Hospital System

banate hain.

---

# 2. End Users

Ye wo users hote hain jo applications use karte hain.

---

# Types of End Users

## A. Naïve Users

Simple users jo sirf application use karte hain.

### Example

ATM User

---

## B. Sophisticated Users

Advanced users jo directly database access kar sakte hain.

### Example

Data Analyst

---

# 3. Database Administrator (DBA)

DBA database ka manager hota hai.

---

# Responsibilities of DBA

- Database maintain karna
- Backup lena
- User permissions dena
- Recovery perform karna
- Security maintain karna

---

# Real Life Example

Bank DBA ensure karta hai:

- Transactions properly work karein
- Backup available ho
- Data secure rahe

---

# Duties of DBA

# 1. Schema Design

Database structure create karna.

---

# 2. Granting Access

Users ko permissions dena.

---

# 3. Monitoring Disk Space

Storage usage monitor karna.

---

# 4. Monitoring Running Jobs

System ki activities monitor karna.

---

# Components of Database Environment

# 1. Database

Data ko store karta hai.

---

# 2. DBMS

Database ko manage karta hai.

---

# 3. Application Programs

Users aur DBMS ke darmiyan communication karte hain.

---

# 4. Database Designers

Database structure design karte hain.

---

# 5. Database Administrator

Database ko maintain aur secure karta hai.

---

# Summary

Is lecture me humne seekha:

- Data aur Information ka difference
- Schema aur Metadata
- DBMS aur uske functions
- Advantages aur disadvantages of database systems
- Importance of data
- Levels of data
- Types of database users
- Responsibilities of DBA

---

# Important Short Definitions

| Term | Definition |
|---|---|
| Data | Raw facts |
| Information | Processed meaningful data |
| Schema | Database structure |
| Metadata | Data about data |
| DBMS | Software that manages database |
| DBA | Person who manages database |
| Consistency | Same data at all places |
| Concurrency | Multiple users accessing database simultaneously |
