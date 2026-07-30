# 📚 DBMS — Lecture 26
# SQL Commands & DDL — CREATE Command

---

## 📖 Lecture Overview

Pichli lectures mein hum ne:

- Examination System ka database dekha
- ER Model banaya
- Relational Model banaya
- Database ko normalize kiya

Ab hum **SQL (Structured Query Language)** ke different commands parhna shuru kar rahe hain.

Is lecture mein specially hum **DDL (Data Definition Language)** aur us ki important command **CREATE** ko detail mein parhenge.

---

# 🔹 SQL Kya Hai?

SQL ka full form hai:

> **Structured Query Language**

SQL ek language hai jo databases ke saath kaam karne ke liye use hoti hai.

SQL ki madad se hum:

- Database create kar sakte hain
- Tables create kar sakte hain
- Data insert kar sakte hain
- Data update kar sakte hain
- Data delete kar sakte hain
- Data search/retrieve kar sakte hain
- Users ko permissions de sakte hain

### Simple Example

```text
University Database
        |
        +---- Student Table
        |
        +---- Teacher Table
        |
        +---- Course Table
        |
        +---- Exam Table
```

---

# 🔹 SQL Commands ki Categories

SQL commands ko major categories mein divide kiya jata hai:

| Category | Full Form | Purpose |
|---|---|---|
| DDL | Data Definition Language | Database ki structure define karna |
| DML | Data Manipulation Language | Data ko manipulate karna |
| DCL | Data Control Language | Permissions aur access control |
| TCL | Transaction Control Language | Transactions manage karna |

> ⚠️ Is lecture mein hamara main focus **DDL** par hai.

---

# 🟢 DDL — Data Definition Language

DDL ka full form hai:

> **Data Definition Language**

DDL ka kaam database ki **structure define aur modify** karna hota hai.

Simple words mein:

> DDL batati hai ke database ka structure kaisa hoga.

DDL ke through hum define kar sakte hain:

1. Tables
2. Columns
3. Data Types
4. Constraints
5. Indexes
6. Views
7. Database Structure

---

# 🔹 DDL ka Real-Life Example

Sochiye hum ek university ka database bana rahe hain.

Sab se pehle hum database create karenge:

```sql
CREATE DATABASE University;
```

Phir Student table:

```sql
CREATE TABLE Student
(
    student_id INT,
    student_name VARCHAR(50),
    semester INT
);
```

Yahan hum database aur table ka **structure** define kar rahe hain.

Is liye `CREATE` DDL command hai.

---

# 🔹 DDL ke Important Commands

DDL mein commonly following commands hoti hain:

| Command | Kaam |
|---|---|
| CREATE | New object create karna |
| ALTER | Existing structure modify karna |
| DROP | Object ko completely remove karna |
| TRUNCATE | Table ka data remove karna |

Is lecture mein hum specially:

> **CREATE**

ko detail mein parhenge.

---

# 🟢 CREATE Command

`CREATE` command ka use kisi **new database object** ko create karne ke liye hota hai.

CREATE se hum:

- Database create kar sakte hain
- Table create kar sakte hain
- View create kar sakte hain
- Index create kar sakte hain

---

# 🟢 CREATE DATABASE

Database create karne ke liye:

```sql
CREATE DATABASE database_name;
```

### Example

```sql
CREATE DATABASE EXAM;
```

Is command se:

```text
EXAM
```

naam ka database create ho jayega.

---

# 🔹 Real-Life Example — University

```sql
CREATE DATABASE University;
```

Ab hamare paas:

```text
University
    |
    +--- Student
    +--- Teacher
    +--- Course
    +--- Exam
```

jaise tables create karne ke liye database ready hai.

---

# 🔹 Database aur Table mein Difference

| Database | Table |
|---|---|
| Database ek container hota hai | Table database ke andar hoti hai |
| Is mein multiple tables ho sakti hain | Is mein rows aur columns hote hain |
| Example: EXAM | Example: Student |

Example:

```text
EXAM Database
     |
     +--- Student Table
     |
     +--- Course Table
     |
     +--- Teacher Table
     |
     +--- Result Table
```

---

# 🟢 CREATE TABLE

Table create karne ke liye:

```sql
CREATE TABLE table_name
(
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

---

# 🔹 Basic Example

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    stName VARCHAR(50),
    cgpa REAL
);
```

Yahan:

| Part | Meaning |
|---|---|
| Student | Table Name |
| stId | Column |
| CHAR(5) | Data Type |
| stName | Column |
| VARCHAR(50) | Data Type |
| cgpa | Column |
| REAL | Data Type |

---

# 🔹 Table Name

Har table ka ek unique aur valid naam hona chahiye.

Examples:

```text
Student
Teacher
Course
Department
Exam
Airport
Employee
Customer
```

### Good Naming Example

```sql
CREATE TABLE Student;
```

### Meaningful Names Use Karein

❌ T1

❌ ABC

✅ Student

✅ Course

✅ Employee

Meaningful name se database ko samajhna easy hota hai.

---

# 🔹 Column Names

Table ke andar multiple columns ho sakte hain.

Example:

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    stName VARCHAR(50),
    stPhone VARCHAR(15),
    cgpa REAL
);
```

Columns:

```text
stId
stName
stPhone
cgpa
```

---

# 🟢 Data Types

Har column ko ek suitable data type dena zaroori hota hai.

Data type batata hai:

> Column mein kis type ka data store hoga.

---

# 🔹 Common Data Types

| Data Type | Meaning | Example |
|---|---|---|
| CHAR | Fixed length text | `S0001` |
| VARCHAR | Variable length text | `Ali Ahmed` |
| INT | Integer number | `10` |
| TINYINT | Small integer | `5` |
| SMALLINT | Small integer | `20` |
| REAL | Decimal/floating value | `3.45` |
| TEXT | Large text | Address |

---

# 🔹 CHAR vs VARCHAR

### CHAR

CHAR fixed length hota hai.

Example:

```sql
stId CHAR(5)
```

Agar value:

```text
S0001
```

hai to length 5 hai.

---

### VARCHAR

VARCHAR variable length hota hai.

Example:

```sql
stName VARCHAR(50)
```

Agar name hai:

```text
Ali
```

to 50 characters ki zaroorat nahi hogi.

---

# 🟢 Example — Program Table

Lecture mein Program table ka example:

```sql
CREATE TABLE Program
(
    prName CHAR(4),
    totSem TINYINT,
    prCredits SMALLINT
);
```

### Table Structure

| Column | Data Type | Meaning |
|---|---|---|
| prName | CHAR(4) | Program Name |
| totSem | TINYINT | Total Semesters |
| prCredits | SMALLINT | Total Credits |

Example records:

| prName | totSem | prCredits |
|---|---:|---:|
| BSCS | 8 | 133 |
| BSSE | 8 | 135 |
| BBA | 8 | 132 |

---

# 🟢 Student Table Example

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    stName CHAR(25),
    stFName CHAR(25),
    stAdres TEXT,
    stPhone CHAR(10),
    prName CHAR(4),
    curSem SMALLINT,
    cgpa REAL
);
```

### Is table ka purpose

Yeh table students ki information store karegi.

| Column | Meaning |
|---|---|
| stId | Student ID |
| stName | Student Name |
| stFName | Father's Name |
| stAdres | Address |
| stPhone | Phone Number |
| prName | Program |
| curSem | Current Semester |
| cgpa | CGPA |

---

# 🟢 Constraints

Constraint ka matlab hai:

> Database mein lagaya gaya ek rule jo data ko valid rakhne mein help karta hai.

Constraints ka purpose:

- Invalid data ko rokna
- Duplicate data ko control karna
- Relationships maintain karna
- Data consistency improve karna

---

# 🔹 Important Constraints

SQL mein commonly following constraints use hoti hain:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# 🟢 1. PRIMARY KEY

Primary Key table ki har row ko uniquely identify karti hai.

### Example

```sql
CREATE TABLE Student
(
    stId CHAR(5) PRIMARY KEY,
    stName VARCHAR(50)
);
```

Yahan:

```text
stId = Primary Key
```

---

## Primary Key ka Example

| stId | stName |
|---|---|
| S0001 | Ali |
| S0002 | Ahmed |
| S0003 | Sara |

Har student ka ID unique hai.

---

## Primary Key ke Rules

Primary Key:

- Duplicate nahi ho sakti
- NULL nahi ho sakti
- Har row ko uniquely identify karti hai

### Invalid Example

| stId | stName |
|---|---|
| S0001 | Ali |
| S0001 | Ahmed ❌ |

Same `stId` dobara use nahi ho sakti.

---

# 🟢 2. NOT NULL

`NOT NULL` ka matlab:

> Is column mein value dena zaroori hai.

Example:

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    stName VARCHAR(50) NOT NULL
);
```

Yahan `stName` empty/null nahi chhoda ja sakta.

---

### Real-Life Example

Student ka naam compulsory hai:

```sql
stName VARCHAR(50) NOT NULL
```

Lekin address optional ho sakta hai:

```sql
address VARCHAR(100)
```

---

# 🟢 3. UNIQUE

`UNIQUE` ka purpose duplicate values ko prevent karna hai.

Example:

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    email VARCHAR(100) UNIQUE
);
```

Ab do students ka same email nahi ho sakta.

### Example

| stId | email |
|---|---|
| S0001 | ali@gmail.com |
| S0002 | sara@gmail.com |
| S0003 | ali@gmail.com ❌ |

Third record invalid hoga kyun ke email duplicate hai.

---

# 🟢 4. CHECK

`CHECK` constraint kisi condition ko enforce karti hai.

Example:

```sql
cgpa REAL CHECK (cgpa >= 0)
```

Matlab:

```text
CGPA 0 se kam nahi ho sakti.
```

---

## Real-Life Example

Agar university mein CGPA 0 se 4 ke darmiyan hai:

```sql
cgpa REAL CHECK (cgpa >= 0 AND cgpa <= 4)
```

Ab:

```text
3.5 ✅
2.8 ✅
4.0 ✅
5.0 ❌
-1.0 ❌
```

---

# 🟢 5. DEFAULT

`DEFAULT` ka matlab:

> Agar user value provide na kare to database automatically ek default value store kar dega.

Example:

```sql
curSem SMALLINT DEFAULT 1
```

Agar semester mention nahi kiya gaya:

```text
curSem = 1
```

automatically store ho jayega.

---

## Real-Life Example

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    stName VARCHAR(50),
    curSem INT DEFAULT 1
);
```

Agar hum insert karein:

```sql
INSERT INTO Student(stId, stName)
VALUES ('S0001', 'Ali');
```

to `curSem` automatically:

```text
1
```

ho jayega.

---

# 🟢 6. FOREIGN KEY

Foreign Key tables ke darmiyan relationship establish karti hai.

Example:

### Program Table

```sql
CREATE TABLE Program
(
    prName CHAR(4) PRIMARY KEY
);
```

### Student Table

```sql
CREATE TABLE Student
(
    stId CHAR(5) PRIMARY KEY,
    stName VARCHAR(50),
    prName CHAR(4),

    FOREIGN KEY (prName)
    REFERENCES Program(prName)
);
```

Ab Student ka `prName` Program table ke existing `prName` ko reference karega.

---

# 🔹 Foreign Key ka Real-Life Example

### Program

| prName |
|---|
| BSCS |
| BSSE |
| BBA |

### Student

| stId | stName | prName |
|---|---|---|
| S0001 | Ali | BSCS |
| S0002 | Sara | BSSE |
| S0003 | Ahmed | BBA |

Agar koi student:

```text
prName = XYZ
```

enter kare aur Program table mein `XYZ` exist na karta ho, to problem hogi.

Foreign Key database ko invalid relationship se bachati hai.

---

# 🟢 Constraint Naming

Lecture mein ek important concept hai:

> Har constraint ko meaningful naam dena chahiye.

Example:

```sql
CONSTRAINT ST_PK PRIMARY KEY
```

Yahan:

```text
ST_PK
```

constraint ka naam hai.

Isi tarah:

```sql
CONSTRAINT ST_CK CHECK (...)
```

Yahan:

```text
ST_CK
```

CHECK constraint ka naam hai.

---

# 🔹 Constraint Names kyun Important hain?

Meaningful names se:

- Constraint ko easily identify kar sakte hain
- Error messages samajhna easy hota hai
- Baad mein constraint ko refer karna easy hota hai
- Database administration simple hoti hai

### Example

```text
ST_PK
ST_CK
ST_FK
ST_UQ
```

---

# 🟢 CREATE TABLE with Multiple Constraints

Ab ek complete Student table banate hain:

```sql
CREATE TABLE Student
(
    stId CHAR(5)
        CONSTRAINT ST_PK PRIMARY KEY,

    stName VARCHAR(50)
        CONSTRAINT ST_NN NOT NULL,

    stFName VARCHAR(50),

    stPhone VARCHAR(15),

    prName CHAR(4),

    curSem SMALLINT
        CONSTRAINT ST_DF DEFAULT 1,

    cgpa REAL
        CONSTRAINT ST_CK CHECK (cgpa >= 0 AND cgpa <= 4)
);
```

---

# 🔹 Student Table ko Samjhein

### Student ID

```sql
stId CHAR(5)
CONSTRAINT ST_PK PRIMARY KEY
```

Meaning:

- ID 5 characters ki hogi
- ID unique hogi
- NULL nahi hogi

---

### Student Name

```sql
stName VARCHAR(50)
CONSTRAINT ST_NN NOT NULL
```

Meaning:

- Name maximum 50 characters
- Name mandatory hai

---

### Current Semester

```sql
curSem SMALLINT
CONSTRAINT ST_DF DEFAULT 1
```

Meaning:

- Agar semester na diya jaye
- To default semester 1 hoga

---

### CGPA

```sql
cgpa REAL
CONSTRAINT ST_CK CHECK (cgpa >= 0 AND cgpa <= 4)
```

Meaning:

```text
0 ≤ CGPA ≤ 4
```

honi chahiye.

---

# 🟢 Student Table with Foreign Key

Agar Student aur Program tables ko connect karna ho:

### Step 1 — Program Table

```sql
CREATE TABLE Program
(
    prName CHAR(4)
        CONSTRAINT PR_PK PRIMARY KEY,

    totSem TINYINT,

    prCredits SMALLINT
);
```

### Step 2 — Student Table

```sql
CREATE TABLE Student
(
    stId CHAR(5)
        CONSTRAINT ST_PK PRIMARY KEY,

    stName VARCHAR(50)
        CONSTRAINT ST_NN NOT NULL,

    stFName VARCHAR(50),

    stPhone VARCHAR(15),

    prName CHAR(4),

    curSem SMALLINT
        CONSTRAINT ST_DF DEFAULT 1,

    cgpa REAL
        CONSTRAINT ST_CK CHECK (cgpa >= 0 AND cgpa <= 4),

    CONSTRAINT ST_FK
        FOREIGN KEY (prName)
        REFERENCES Program(prName)
);
```

---

# 🔹 Constraint Summary Table

| Constraint | Purpose | Example |
|---|---|---|
| PRIMARY KEY | Unique record identify karna | `stId` |
| NOT NULL | Value compulsory karna | `stName` |
| UNIQUE | Duplicate prevent karna | `email` |
| FOREIGN KEY | Tables ka relationship | `prName` |
| CHECK | Condition enforce karna | `cgpa <= 4` |
| DEFAULT | Automatic default value | `curSem = 1` |

---

# 🟢 Complete Exam System Example

Ab hum ek small **Exam System Database** design karte hain.

---

## Step 1 — Database Create Karein

```sql
CREATE DATABASE EXAM;
```

---

## Step 2 — Program Table Create Karein

```sql
CREATE TABLE Program
(
    prName CHAR(4)
        CONSTRAINT PR_PK PRIMARY KEY,

    totSem TINYINT
        CONSTRAINT PR_SEM_CK CHECK (totSem > 0),

    prCredits SMALLINT
        CONSTRAINT PR_CR_CK CHECK (prCredits > 0)
);
```

---

## Step 3 — Student Table Create Karein

```sql
CREATE TABLE Student
(
    stId CHAR(5)
        CONSTRAINT ST_PK PRIMARY KEY,

    stName VARCHAR(50)
        CONSTRAINT ST_NN NOT NULL,

    stFName VARCHAR(50),

    stPhone VARCHAR(15),

    prName CHAR(4),

    curSem SMALLINT
        CONSTRAINT ST_DF DEFAULT 1,

    cgpa REAL
        CONSTRAINT ST_CK CHECK (cgpa >= 0 AND cgpa <= 4),

    CONSTRAINT ST_FK
        FOREIGN KEY (prName)
        REFERENCES Program(prName)
);
```

---

# 🔹 Sample Data

Program table mein:

```sql
INSERT INTO Program
VALUES
('BSCS', 8, 133),
('BSSE', 8, 135),
('BBA', 8, 132);
```

Student table mein:

```sql
INSERT INTO Student
(stId, stName, stFName, stPhone, prName, curSem, cgpa)
VALUES
('S0001', 'Ali', 'Ahmed', '03001234567', 'BSCS', 3, 3.45);

INSERT INTO Student
(stId, stName, stFName, stPhone, prName, curSem, cgpa)
VALUES
('S0002', 'Sara', 'Khan', '03007654321', 'BSSE', 4, 3.80);
```

---

# 🔹 Result

Student table kuch is tarah nazar aa sakti hai:

| stId | stName | stFName | stPhone | prName | curSem | cgpa |
|---|---|---|---|---|---:|---:|
| S0001 | Ali | Ahmed | 03001234567 | BSCS | 3 | 3.45 |
| S0002 | Sara | Khan | 03007654321 | BSSE | 4 | 3.80 |

---

# 🟢 CHECK Constraint ka Practical Test

Agar hum likhein:

```sql
INSERT INTO Student
(stId, stName, prName, curSem, cgpa)
VALUES
('S0003', 'Ahmed', 'BSCS', 2, 5.5);
```

To record reject ho sakta hai kyun ke:

```text
cgpa <= 4
```

condition apply ki gayi hai.

---

# 🟢 PRIMARY KEY ka Practical Test

Agar pehle se:

```text
S0001
```

exist karta hai aur hum dobara:

```sql
INSERT INTO Student
(stId, stName)
VALUES
('S0001', 'Usman');
```

karein to duplicate Primary Key ki wajah se error aayega.

---

# 🟢 NOT NULL ka Practical Test

Agar:

```sql
stName VARCHAR(50) NOT NULL
```

hai aur hum:

```sql
INSERT INTO Student(stId)
VALUES ('S0004');
```

karein to error aayega kyun ke student name required hai.

---

# 🟢 DEFAULT ka Practical Test

Agar:

```sql
curSem SMALLINT DEFAULT 1
```

hai aur hum:

```sql
INSERT INTO Student(stId, stName)
VALUES ('S0005', 'Hina');
```

karein to:

```text
curSem = 1
```

automatically set ho jayega.

---

# 🔹 SQL Server Example

Lecture mein SQL Server ka reference diya gaya hai.

Agar SQL Server mein kaam kar rahe hon to queries SQL Server ke Query Editor / Query Analyzer mein execute ki ja sakti hain.

Example:

```sql
CREATE DATABASE EXAM;
```

Database create karne ke baad us database ko use karke tables create ki ja sakti hain.

---

# 🧠 Important Difference: Database vs Table vs Row vs Column

## Database

Complete container.

```text
EXAM
```

## Table

Database ke andar structure.

```text
Student
```

## Column

Student ki property.

```text
stId
stName
cgpa
```

## Row

Ek complete student ka record.

```text
S0001 | Ali | 3.45
```

Visual form:

```text
DATABASE
   |
   +---- TABLE
           |
           +---- COLUMNS
           |      |
           |      +--- stId
           |      +--- stName
           |      +--- cgpa
           |
           +---- ROWS
                  |
                  +--- S0001, Ali, 3.45
```

---

# 🔹 DDL aur DML mein Difference

| DDL | DML |
|---|---|
| Structure ke saath deal karti hai | Data ke saath deal karti hai |
| Table create karti hai | Data insert karti hai |
| `CREATE` | `INSERT` |
| `ALTER` | `UPDATE` |
| `DROP` | `DELETE` |
| Database structure define karti hai | Data manipulate karti hai |

### Example

DDL:

```sql
CREATE TABLE Student
(
    stId INT,
    stName VARCHAR(50)
);
```

DML:

```sql
INSERT INTO Student
VALUES (1, 'Ali');
```

---

# 📌 Important Exam Questions

## Q1. DDL kya hai?

**Answer:**

DDL ka full form **Data Definition Language** hai. Is ka use database ki structure define aur manage karne ke liye hota hai.

---

## Q2. CREATE command kya karti hai?

**Answer:**

CREATE command new database objects create karne ke liye use hoti hai, jaise:

- Database
- Table
- View
- Index

---

## Q3. CREATE DATABASE ka syntax?

```sql
CREATE DATABASE database_name;
```

Example:

```sql
CREATE DATABASE EXAM;
```

---

## Q4. CREATE TABLE ka syntax?

```sql
CREATE TABLE table_name
(
    column1 datatype,
    column2 datatype
);
```

---

## Q5. Primary Key kya hoti hai?

Primary Key table ki har row ko uniquely identify karti hai.

Primary Key mein:

- Duplicate values allowed nahi hoti
- NULL allowed nahi hota

---

## Q6. NOT NULL kya karta hai?

`NOT NULL` ensure karta hai ke column mein value lazmi provide ki jaye.

---

## Q7. CHECK constraint kya karti hai?

CHECK constraint kisi value par condition enforce karti hai.

Example:

```sql
CHECK (cgpa >= 0 AND cgpa <= 4)
```

---

## Q8. DEFAULT kya hota hai?

Agar user value provide na kare to DEFAULT constraint automatically predefined value store karta hai.

Example:

```sql
curSem SMALLINT DEFAULT 1
```

---

## Q9. FOREIGN KEY kya hoti hai?

Foreign Key ek table ke column ko doosri table ke column ke saath relate karti hai aur referential integrity maintain karti hai.

---

## Q10. UNIQUE aur PRIMARY KEY mein difference?

| PRIMARY KEY | UNIQUE |
|---|---|
| Row ko uniquely identify karti hai | Duplicate values prevent karti hai |
| NULL allowed nahi | DBMS ke rules ke mutabiq NULL handling different ho sakti hai |
| Usually ek primary key hoti hai | Multiple UNIQUE constraints ho sakti hain |

---

# 🧠 Easy Way to Remember Constraints

Is trick se yaad karein:

```text
PRIMARY KEY
        ↓
"Kaun sa record hai?"

NOT NULL
        ↓
"Value deni zaroori hai?"

UNIQUE
        ↓
"Duplicate nahi hona chahiye"

FOREIGN KEY
        ↓
"Do tables ko connect karo"

CHECK
        ↓
"Condition follow karo"

DEFAULT
        ↓
"Value na mile to default do"
```

---

# 🎯 Real-Life Example — University Database

Sochiye ek university mein Student table hai.

Har student ke paas:

```text
Student ID
Name
Email
Program
Semester
CGPA
```

Rules:

```text
Student ID → Unique
Name → Required
Email → Unique
Program → Existing Program hona chahiye
Semester → Default 1
CGPA → 0 se 4 ke darmiyan
```

SQL:

```sql
CREATE TABLE Student
(
    student_id CHAR(5)
        PRIMARY KEY,

    student_name VARCHAR(50)
        NOT NULL,

    email VARCHAR(100)
        UNIQUE,

    program_id INT,

    semester INT
        DEFAULT 1,

    cgpa REAL
        CHECK (cgpa >= 0 AND cgpa <= 4)
);
```

Yeh real-life database constraints ka perfect example hai.

---

# 🎯 Real-Life Example — Online Shopping

Suppose hum e-commerce website ka Product table banate hain:

```sql
CREATE TABLE Product
(
    product_id INT PRIMARY KEY,

    product_name VARCHAR(100) NOT NULL,

    price REAL CHECK (price > 0),

    stock INT DEFAULT 0,

    product_code VARCHAR(30) UNIQUE
);
```

Yahan:

| Constraint | Purpose |
|---|---|
| PRIMARY KEY | Product ko identify karna |
| NOT NULL | Product name compulsory |
| CHECK | Price 0 se zyada |
| DEFAULT | Stock default 0 |
| UNIQUE | Product code duplicate na ho |

---

# 🎯 Real-Life Example — Employee Database

```sql
CREATE TABLE Employee
(
    employee_id INT PRIMARY KEY,

    employee_name VARCHAR(50) NOT NULL,

    email VARCHAR(100) UNIQUE,

    salary REAL CHECK (salary > 0),

    department VARCHAR(50),

    experience INT DEFAULT 0
);
```

---

# 🔹 CREATE Command ka Complete Structure

Ek table create karte waqt generally:

```text
CREATE TABLE
       ↓
   Table Name
       ↓
   Column Name
       ↓
   Data Type
       ↓
   Constraints
```

Example:

```sql
CREATE TABLE Student
(
    stId CHAR(5) PRIMARY KEY,
    stName VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    cgpa REAL CHECK (cgpa >= 0 AND cgpa <= 4),
    curSem INT DEFAULT 1
);
```

---

# 📝 Lecture Summary

Lecture 26 mein hum ne SQL ke **DDL** concept ko samjha.

DDL ka full form:

> **Data Definition Language**

DDL database ki structure define karti hai.

Is lecture mein sab se important command:

> **CREATE**

parhi gayi.

CREATE command se:

- Database create hota hai
- Table create hoti hai
- Columns define hote hain
- Data types define hote hain
- Constraints apply ki ja sakti hain

Important constraints:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# ⭐ Most Important Syntaxes

## Create Database

```sql
CREATE DATABASE EXAM;
```

---

## Create Table

```sql
CREATE TABLE Student
(
    stId CHAR(5),
    stName VARCHAR(50),
    cgpa REAL
);
```

---

## Primary Key

```sql
stId CHAR(5) PRIMARY KEY
```

---

## NOT NULL

```sql
stName VARCHAR(50) NOT NULL
```

---

## UNIQUE

```sql
email VARCHAR(100) UNIQUE
```

---

## CHECK

```sql
cgpa REAL CHECK (cgpa >= 0 AND cgpa <= 4)
```

---

## DEFAULT

```sql
curSem INT DEFAULT 1
```

---

## FOREIGN KEY

```sql
FOREIGN KEY (prName)
REFERENCES Program(prName)
```

---

# ✅ Final Practice Question

**Exam System ka database create karein aur Student table banayein jismein following constraints hon:**

- Student ID → Primary Key
- Student Name → NOT NULL
- Email → UNIQUE
- Semester → DEFAULT 1
- CGPA → CHECK 0 se 4 ke darmiyan
- Program → FOREIGN KEY

### Solution

```sql
CREATE DATABASE EXAM;
```

Program table:

```sql
CREATE TABLE Program
(
    prName CHAR(4)
        CONSTRAINT PR_PK PRIMARY KEY,

    totSem TINYINT,

    prCredits SMALLINT
);
```

Student table:

```sql
CREATE TABLE Student
(
    stId CHAR(5)
        CONSTRAINT ST_PK PRIMARY KEY,

    stName VARCHAR(50)
        CONSTRAINT ST_NN NOT NULL,

    email VARCHAR(100)
        CONSTRAINT ST_UQ UNIQUE,

    prName CHAR(4),

    curSem SMALLINT
        CONSTRAINT ST_DF DEFAULT 1,

    cgpa REAL
        CONSTRAINT ST_CK CHECK
        (cgpa >= 0 AND cgpa <= 4),

    CONSTRAINT ST_FK
        FOREIGN KEY (prName)
        REFERENCES Program(prName)
);
```

---

# 🎓 Quick Revision

```text
SQL
│
├── DDL
│   ├── CREATE
│   ├── ALTER
│   ├── DROP
│   └── TRUNCATE
│
├── DML
│   ├── INSERT
│   ├── UPDATE
│   ├── DELETE
│   └── SELECT
│
└── DCL
    ├── GRANT
    └── REVOKE
```

### CREATE

```text
CREATE DATABASE
        ↓
CREATE TABLE
        ↓
Columns + Data Types
        ↓
Constraints
        ↓
Valid Database Structure
```

---

# 💡 One-Line Concepts

> **DDL = Database ki structure**

> **CREATE = New object banana**

> **TABLE = Rows + Columns**

> **PRIMARY KEY = Unique identity**

> **FOREIGN KEY = Tables ka relationship**

> **NOT NULL = Value compulsory**

> **UNIQUE = Duplicate allowed nahi**

> **CHECK = Condition**

> **DEFAULT = Automatic value**
