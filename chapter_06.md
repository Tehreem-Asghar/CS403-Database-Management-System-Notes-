# Lecture No. 06 — Database Design Phase & Data Models

# Introduction

Database Design Phase, Analysis Phase ke baad aati hai.  
Is phase me database ka proper structure design kiya jata hai taake users ki requirements ko efficiently fulfill kiya ja sake.

Database designing kisi bhi database system ka bohat important part hota hai kyunki agar database properly design na ho to:

- Data duplicate ho sakta hai
- Queries slow ho sakti hain
- System errors aa sakte hain
- Reports incorrect ban sakti hain

---

# Database Design / Database Model

Database Design ya Database Model database ki logical structure ko represent karta hai.

Ye batata hai:

- Data kis form me store hoga
- Data ke relationships kya honge
- Different tables ya entities ka connection kya hoga

Database design ko database schema me store kiya jata hai aur schema Data Dictionary me save hota hai.

---

# Real Life Example

Agar hum ek **School Management System** bana rahe hain to database me ye cheezen hongi:

| Student Table | Course Table | Result Table |
|---|---|---|
| studentId | courseId | resultId |
| studentName | courseName | marks |
| class | creditHours | grade |

In tables ke darmiyan relationships hongi:

- Student courses enroll karega
- Student ka result generate hoga
- Course multiple students ko assign hoga

Ye tamam structure Database Design ka part hota hai.

---

# Database Modeling

Database ki logical structure create karne ke process ko Database Modeling kehte hain.

Database Modeling me hum decide karte hain:

- Konsi entities hongi
- Konsi attributes hongi
- Konsi relationships hongi

Generally design graphical form me banayi jati hai taake system easily samajh aaye.

---

# Real Life Example

University Database Modeling:

## Entities

- Student
- Teacher
- Course
- Department

## Relationships

- Student enrolls in Course
- Teacher teaches Course
- Department manages Teachers

---

# Data Model

Data Model ek set of rules aur constructs hota hai jo database design create karne ke liye use hota hai.

Data Model define karta hai:

- Data ka structure
- Data manipulation
- Data constraints

---

# Components of Data Model

## 1. Structure

Ye define karta hai ke data kis structure me store hoga.

### Example Structures

- Tables
- Records
- Objects
- Trees

### Real Life Example

Student table:

| studentId | studentName | class |
|---|---|---|
| 101 | Ali | BSCS |

Ye ek structure hai.

---

# 2. Manipulation Language

Ye language data ko manipulate karne ke liye use hoti hai.

Manipulation ka matlab:

- Insert
- Update
- Delete
- Retrieve

### Example

SQL language:

```sql
SELECT * FROM Students;
```

Ye student data retrieve karega.

---

# 3. Integrity Constraints

Ye rules database ki correctness maintain karte hain.

Ye ensure karte hain ke:

- Wrong data enter na ho
- Duplicate data na aaye
- Relationships correct rahen

---

# Real Life Examples of Constraints

## Primary Key

```sql
studentId INT PRIMARY KEY
```

Har student ka unique ID hoga.

---

## NOT NULL Constraint

```sql
studentName VARCHAR(50) NOT NULL
```

Student ka naam empty nahi ho sakta.

---

## Foreign Key

```sql
courseId INT REFERENCES Courses(courseId)
```

Sirf valid course hi assign ho sakta hai.

---

# Significance of Data Model

Data Model bohat important hai kyunki:

- Har DBMS kisi na kisi data model par based hota hai
- Proper database design isi ki madad se hoti hai
- Data efficiently organize hota hai

Agar hume data model ka knowledge na ho to:

- Proper database create nahi kar sakte
- Relationships design nahi kar sakte
- Constraints apply nahi kar sakte

---

# Types of Data Models

Data Models ki do main categories hoti hain:

1. Semantic Data Model
2. Record Based Data Model

---

# 1. Semantic Data Model

Ye models database ko zyada meaningful aur flexible banate hain.

Ye better facilities provide karte hain:

- Constraints
- Relationships
- Data structures

Semantic Models zyada tar conceptual designing ke liye use hote hain.

---

# Types of Semantic Data Models

## ER Data Model

## Object Oriented Data Model

---

# ER (Entity Relationship) Data Model

ER Model database designing ka bohat famous model hai.

Is me:

- Entities
- Attributes
- Relationships

show kiye jate hain.

---

# Real Life Example of ER Model

## Entities

### Student

- studentId
- studentName

### Course

- courseId
- courseName

## Relationship

Student "enrolls in" Course

---

# Simple ER Diagram Idea

```text
Student -------- Enrolls -------- Course
```

---

# Object Oriented Data Model

Ye model object-oriented programming concepts use karta hai.

Is me:

- Objects
- Classes
- Methods

hote hain.

---

# Real Life Example

Agar hum banking system bana rahe hain:

## Object: Account

Properties:

- accountNumber
- balance

Methods:

- deposit()
- withdraw()

---

# 2. Record Based Data Model

Ye models records ki form me data handle karte hain.

Is ki 3 types hoti hain:

- Hierarchical Data Model
- Network Data Model
- Relational Data Model

---

# Hierarchical Data Model

Ye tree structure follow karta hai.

Parent-child relationship hoti hai.

Ek parent ke multiple children ho sakte hain.

---

# Real Life Example

```text
University
 ├── Department
      ├── Teacher
           ├── Student
```

---

# Network Data Model

Ye model graph structure use karta hai.

Is me many-to-many relationships possible hoti hain.

---

# Real Life Example

Ek student multiple courses le sakta hai aur ek course multiple students ko diya ja sakta hai.

```text
Student <------> Course
```

---

# Relational Data Model

Ye sab se famous aur modern model hai.

Is me data tables ki form me store hota hai.

Ye SQL databases me use hota hai.

---

# Real Life Example

## Students Table

| studentId | studentName |
|---|---|
| 1 | Ali |

## Courses Table

| courseId | courseName |
|---|---|
| 101 | Database |

## Enrollment Table

| studentId | courseId |
|---|---|
| 1 | 101 |

---

# Important Point

ER Model sirf designing ke liye use hota hai.

Koi DBMS directly ER Model par based nahi hota.

Lekin bohat se DBMS:

- Relational Model
- Object Oriented Model
- Hierarchical Model

par based hote hain.

---

# Types of Database Design

Database Design ki 3 main levels hoti hain:

1. Conceptual Database Design
2. Logical Database Design
3. Physical Database Design

---

# 1. Conceptual Database Design

Ye high-level design hoti hai.

Is me hum sirf overall structure aur relationships define karte hain.

Mostly ER Model use hota hai.

---

# Real Life Example

University system me:

- Student
- Teacher
- Course

entities define karna conceptual design hai.

---

# 2. Logical Database Design

Is phase me conceptual model ko actual data model me convert kiya jata hai.

Mostly relational tables banayi jati hain.

---

# Real Life Example

## Student Table

| studentId | studentName |

## Course Table

| courseId | courseName |

---

# 3. Physical Database Design

Is phase me database ko actual DBMS software me implement kiya jata hai.

---

# Real Life Example

MySQL me tables create karna:

```sql
CREATE TABLE Students(
    studentId INT PRIMARY KEY,
    studentName VARCHAR(50)
);
```

---

# Benefits of Separating Database Design Levels

Different levels separate rakhne ke bohat fayde hain:

## 1. Better Abstraction

Har level ka kaam separate hota hai.

---

## 2. Easy Understanding

System ko samajhna easy ho jata hai.

---

## 3. Flexibility

Future me DBMS change karna easy ho jata hai.

---

# Real Life Example

Agar pehle database Oracle me tha aur baad me MySQL me shift karna ho to:

- Conceptual design same rehegi
- Logical design mostly same rehegi
- Sirf physical implementation change hogi

---

# Data Dictionary

Data Dictionary ek aisi database hoti hai jo database system ke bare me information store karti hai.

Ye metadata store karti hai.

---

# Data Dictionary me Kya Store Hota Hai?

- Schemas
- File specifications
- Data locations
- User permissions
- Reports information

---

# Types of Data Dictionary

1. Integrated Data Dictionary
2. Free Standing Data Dictionary

---

# Integrated Data Dictionary

Ye DBMS ke andar built-in hoti hai.

DBMS khud isay manage karta hai.

---

# Example

Oracle aur MySQL ki internal system catalogs.

---

# Free Standing Data Dictionary

Ye external CASE tools ke through create hoti hai.

Baad me DBMS ke sath attach hoti hai.

---

# Cross Reference Matrix (CRM)

CRM ek tool hai jo attributes aur reports ke relationships ko identify karta hai.

---

# CRM ka Purpose

Ye batata hai:

- Konsa attribute kis report me use ho raha hai
- Konsi entities related hain

---

# Real Life Example

| Attribute | Transcript | Result Card |
|---|---|---|
| studentName | ✓ | ✓ |
| marks | ✓ | ✓ |
| grade | ✓ | ✓ |

---

# Analysis Phase Outcome

Analysis phase me designers:

- User requirements analyze karte hain
- DFDs create karte hain
- Initial database design prepare karte hain

---

# Flow of Phases

```text
Preliminary Study
        ↓
DFDs
        ↓
Analysis Phase
        ↓
Initial Database Design
        ↓
Database Design Phase
        ↓
Final Database
```

---

# Summary

- Database Design database ki structure define karta hai
- Database Modeling structure create karne ka process hai
- Data Model database design ka framework hota hai
- Semantic aur Record Based models important categories hain
- ER Model conceptual designing ke liye famous hai
- Relational Model sab se zyada use hota hai
- Database design ki 3 levels hoti hain:
  - Conceptual
  - Logical
  - Physical
- Data Dictionary metadata store karti hai
- CRM attributes aur reports ke relations identify karta hai
