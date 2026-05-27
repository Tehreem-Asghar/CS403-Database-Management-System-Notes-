# Database Management System (CS403)  
# Lecture No. 03 — Database Architecture Detailed Notes

# Topics Covered

- Database Architecture
- Three Level Schema Architecture
- Internal Level / Internal Schema
- External View / External Schema
- Conceptual / Logical View
- Database Intention
- Database Extension
- Mapping Between Levels
- Real Life Examples

---

# Introduction to Database Architecture

Database Architecture ek structured design hoti hai jo database system ko organize karti hai.

ANSI SPARK ne 1975 me Three Level Architecture introduce ki thi jo aaj bhi worldwide use hoti hai.

Is architecture ka main purpose:

- Data ko organize karna
- Security provide karna
- Different users ko different views dena
- Data independence provide karna

---

# Why Standardization Important Hai?

Standardization future growth ke liye bohat important hoti hai.

## Benefits of Standardization

### 1. Easy Development

Agar naya system banana ho to pehle se defined standards follow kiye ja sakte hain.

### Example

Ek university pehle se student database system use kar rahi hai.

Agar library system banana ho to same standards follow kar ke easily integrate kiya ja sakta hai.

---

### 2. Easy Integration

Additional software ko existing database ke sath connect karna easy hota hai.

### Example

Attendance system ko student management system ke sath connect karna.

---

### 3. Easy for Users

Users ko naye system ko samajhne me asani hoti hai.

### Example

Agar har banking app same type ka interface use kare to users confuse nahi honge.

---

### 4. Easy for Technical Staff

Naya technical staff bina zyada training ke system ko samajh sakta hai.

---

# Three Level Schema Architecture

Three Level Architecture database ko 3 levels me divide karti hai:

1. External Level
2. Conceptual Level
3. Internal Level

---

# Diagram of Three Level Architecture

```text
+----------------------+
|   External Level     |
| (User Views)         |
+----------------------+

+----------------------+
| Conceptual Level     |
| (Logical Structure)  |
+----------------------+

+----------------------+
| Internal Level       |
| (Physical Storage)   |
+----------------------+
```

---

# Purpose of Three Level Architecture

Is architecture ka main purpose hai:

- Data hiding
- Security
- Data independence
- Multiple user views provide karna

---

# 1. Internal Level / Internal Schema

Yeh database architecture ka sabse lowest level hota hai.

Is level par database ki physical storage details define hoti hain.

---

# Internal Schema kya define karta hai?

Internal schema define karta hai:

- Data ka structure
- Data kis format me store hoga
- File organization
- Indexing
- Storage details
- Access permissions

---

# Real Life Example

Agar Student table ho:

| RollNo | Name  | DOB        |
|--------|-------|------------|
| 101    | Ali   | 12-05-2002 |

Internal schema decide karega:

- RollNo integer hoga
- Name string hoga
- DOB date type hogi
- Data disk par kis format me store hoga

---

# Database Intention

Database ki intention ka matlab hai:

Database ka complete design aur structure.

Yeh almost permanent hoti hai.

---

# Example

University database me:

- Student records
- Courses
- Teachers
- Results

store karne ka plan database ki intention hai.

---

# Database Extension

Database me actual data insert karna extension kehlata hai.

---

# Example

## Intention

Student table create karna.

## Extension

Us table me students ka actual data insert karna.

```sql
INSERT INTO Student
VALUES (101, 'Ali', '12-05-2002');
```

---

# Changes at Different Levels

Different levels par changes ka effect different hota hai.

---

# Example

## Extension Change

Agar ek student ka name update ho:

```sql
UPDATE Student
SET Name = 'Ahmed'
WHERE RollNo = 101;
```

Sirf ek record affect hoga.

---

## Internal Schema Change

Agar data type change kar di jaye:

```sql
DOB VARCHAR → DATE
```

To puri table affect ho sakti hai.

---

# External Level / External Schema

External level end users ka level hota hai.

Har user ko uski requirement ke mutabiq data dikhaya jata hai.

---

# External View ka Purpose

- Customized views provide karna
- Security maintain karna
- Easy interface provide karna

---

# Different Users Different Views

Same database ka data different users ko different form me show ho sakta hai.

---

# Example of DOB Formats

Database me DOB stored hai:

```text
28-03-1987
```

Different departments isay different ways me dekhenge:

| Department | Format |
|------------|--------|
| Examination | March-28-1987 |
| Registrar | 03/28/1987 |
| Library | 28/03/87 |

---

# Example of Restricted Access

## Teacher View

Teacher sirf:

- Student Name
- Marks

dekh sakta hai.

---

## Accounts Department View

Accounts department sirf:

- Fee details

dekh sakti hai.

---

# Example of Calculated Data

Database me sirf DOB stored hai.

```text
12-05-2002
```

External view automatically age calculate kar sakta hai.

```text
Current Age = 24 years
```

---

# External View Benefits

- User friendly
- Secure
- Easy navigation
- Unauthorized access rokta hai

---

# Conceptual Level / Logical Schema

Yeh middle level hota hai.

Is level par database ki logical structure define hoti hai.

---

# Conceptual Schema kya store karta hai?

- All entities
- Attributes
- Relationships
- Constraints
- Data types
- Rules

---

# Real Life Company Example

Company database me:

- Customers
- Products
- Stores
- Salespersons
- Managers

sab entities hoti hain.

---

# Relationships Example

## Customer buys Product

```text
Customer → Product
```

## Salesperson works at Outlet

```text
Salesperson → Outlet
```

## Manager manages Salespersons

```text
Manager → Salespersons
```

---

# Conceptual Schema Responsibilities

## 1. Manage Relationships

Entities ke darmiyan relationships maintain karta hai.

---

## 2. Store Constraints

### Example

Student age:

```text
Age >= 18
```

---

## 3. Authorization

Kaun database access karega.

---

## 4. Authentication

Kaun changes kar sakta hai.

---

# Example of Authorization

## Admin

- Add data
- Delete data
- Update data

## Student

- Sirf apna result dekh sakta hai

---

# Mapping Between Levels

Database levels ek doosre ke sath connected hote hain.

---

# External to Conceptual Mapping

External view user request ko conceptual schema se connect karti hai.

---

# Conceptual to Internal Mapping

Conceptual schema data ko physical storage se connect karta hai.

---

# Example of Complete Flow

## Step 1

Student portal open karta hai.

---

## Step 2

External view student ko result show karti hai.

---

## Step 3

Conceptual schema result ki logical structure manage karti hai.

---

## Step 4

Internal schema disk se actual data retrieve karta hai.

---

# Data Independence

Three level architecture data independence provide karti hai.

---

# Types of Data Independence

## 1. Physical Data Independence

Internal storage change karne se users affect nahi hote.

### Example

Hard disk change karna.

---

## 2. Logical Data Independence

Conceptual changes se external views affect nahi hoti.

### Example

New column add karna.

---

# Advantages of Three Level Architecture

| Advantage | Description |
|-----------|-------------|
| Security | Unauthorized access rokta hai |
| Flexibility | Multiple user views |
| Data Independence | Easy changes |
| Easy Maintenance | System manage karna easy |
| Data Hiding | Internal details hide hoti hain |

---

# Summary

## External Level

- User specific views
- Easy interface
- Security

---

## Conceptual Level

- Complete logical structure
- Relationships
- Constraints

---

## Internal Level

- Physical storage
- Data files
- Indexing

---

# Important Exam Points

## Short Questions

- Define External Schema
- Define Conceptual Schema
- Define Internal Schema
- What is database intention?
- What is database extension?

---

# Most Important Difference

| Internal Level | External Level |
|----------------|----------------|
| Physical storage | User view |
| Lowest level | Highest level |
| Technical details | User friendly |

---

# Final Conclusion

Three Level Database Architecture database ko secure, flexible aur manageable banati hai.

Is architecture ki wajah se:

- Same data multiple users ko different forms me dikhaya ja sakta hai
- Internal storage details hide rehti hain
- Database ko easily maintain aur expand kiya ja sakta hai

```
