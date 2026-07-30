```markdown
# 📚 DBMS – Lecture 25
# Structured Query Language (SQL)

---

## 📖 Lecture Overview

Is lecture mein hum **SQL (Structured Query Language)** ke basics parhenge.

Pichli lectures mein humne database ke physical design concepts jaise:

- Partitioning
- Replication

parhe thay.

Ab hum SQL parhna shuru karte hain.

SQL database ke saath communicate karne ke liye use hoti hai. Iski madad se hum database mein data ko:

- dekh sakte hain
- add kar sakte hain
- change kar sakte hain
- delete kar sakte hain
- tables bana sakte hain
- tables remove kar sakte hain
- permissions control kar sakte hain

---

# 🟢 1. SQL Kya Hai?

## SQL ka Full Form

**SQL = Structured Query Language**

SQL aik language hai jo **database se baat karne** ke liye use hoti hai.

Simple words mein:

> SQL ki madad se hum database ko commands dete hain aur database humein required result deta hai.

### Example

Agar `student` naam ki table hai aur humein tamam students dekhne hain:

```sql
SELECT * FROM student;
```

Is command ka simple matlab hai:

> `student` table ka sara data mujhe dikhao.

---

# 🟢 2. SQL Se Hum Kya Kar Sakte Hain?

SQL ki madad se hum database par bohat se operations perform kar sakte hain.

| Operation | SQL Command |
|---|---|
| Data dekhna | SELECT |
| Data add karna | INSERT |
| Data change karna | UPDATE |
| Data delete karna | DELETE |
| Table banana | CREATE |
| Table remove karna | DROP |
| Permission dena | GRANT |
| Permission wapas lena | REVOKE |

### Easy Trick

```text
SELECT  → Data Dekho
INSERT  → Data Add Karo
UPDATE  → Data Change Karo
DELETE  → Data Remove Karo

CREATE  → Naya Object Banao
DROP    → Object Hatao

GRANT   → Permission Do
REVOKE  → Permission Wapas Lo
```

---

# 🟢 3. SQL Ki Main Categories

SQL commands ko different categories mein divide kiya jata hai.

Is lecture mein especially ye concepts important hain:

1. DDL
2. DML
3. Access Control Commands

---

# 🔵 4. DDL – Data Definition Language

## Full Form

**DDL = Data Definition Language**

DDL ka kaam database ki **structure define karna** hota hai.

Yani DDL batati hai:

> Database mein kya structure hoga?

For example:

- kaunsi table hogi
- table ka naam kya hoga
- columns kaun se honge
- columns ke data types kya honge

---

## DDL Ki Example

```sql
CREATE TABLE student (
    stId INT,
    stName VARCHAR(50)
);
```

Yeh command `student` naam ki table create karegi.

### Yahan:

- `CREATE TABLE` → table banane ke liye
- `student` → table ka naam
- `stId` → column
- `INT` → data type
- `stName` → column
- `VARCHAR(50)` → text data type

---

# 🔵 5. DDL Ke Common Commands

Important DDL commands:

```text
CREATE
DROP
```

Kuch SQL systems mein aur bhi DDL commands hoti hain, lekin is lecture ke context mein `CREATE` aur `DROP` important hain.

---

## CREATE

Naya database object create karne ke liye.

Example:

```sql
CREATE TABLE course (
    crCode INT,
    crName VARCHAR(50)
);
```

---

## DROP

Database object ko remove karne ke liye.

Example:

```sql
DROP TABLE course;
```

Iska matlab:

> `course` table ko remove kar do.

⚠️ **Important:**

`DROP` karne se table aur uska structure remove ho jata hai.

---

# 🟢 6. DML – Data Manipulation Language

## Full Form

**DML = Data Manipulation Language**

DML ka kaam database ke andar **stored data ke saath kaam karna** hai.

Yani DML se hum:

- data retrieve karte hain
- data insert karte hain
- data update karte hain
- data delete karte hain

---

# 🔵 DDL Aur DML Mein Difference

| DDL | DML |
|---|---|
| Database ki structure define karti hai | Database ke data ko manipulate karti hai |
| Structure par kaam | Records/data par kaam |
| CREATE | SELECT |
| DROP | INSERT |
|  | UPDATE |
|  | DELETE |

### Easy Example

Socho school mein aik register hai.

### DDL:

Register ka format banana:

```text
Name
Roll No
Class
Marks
```

### DML:

Register mein students ka data:

```text
Ali   101   BSSE   85
Sara  102   BSSE   90
```

Yani:

> **DDL = Structure**

> **DML = Data**

---

# 🟢 7. SQL Syntax Rules

SQL command likhte waqt kuch rules follow kiye jate hain.

---

## Rule 1: Reserved Words Capital Letters Mein

SQL ke reserved words generally uppercase mein likhe jate hain.

Examples:

```sql
SELECT
INSERT
UPDATE
DELETE
CREATE
DROP
FROM
WHERE
```

Example:

```sql
SELECT * FROM student;
```

Yahan:

- `SELECT` reserved keyword hai
- `FROM` reserved keyword hai

---

# 🟢 8. User Defined Identifiers

User-defined identifiers ko generally lowercase mein likha jata hai.

Examples:

```text
student
course
faculty
stName
stId
```

Identifier database object ka naam ho sakta hai.

### Example

```sql
CREATE TABLE student (
    stId INT,
    stName VARCHAR(50)
);
```

Yahan:

- `student` → table identifier
- `stId` → column identifier
- `stName` → column identifier

---

# 🟢 9. Identifier Kya Hota Hai?

Identifier kisi database object ko identify karne wala naam hota hai.

Examples:

- table name
- column name
- variable name

### Example

```text
student
course
faculty
stId
stName
```

Ye sab identifiers ho sakte hain.

---

# 🟢 10. Valid Identifiers

Lecture ke mutabiq identifiers valid hone chahiye.

Identifier:

- `@`
- `_`
- alphabets
- numbers

ko use kar sakta hai.

Lecture mein maximum length **256 characters** di gayi hai.

Aur:

> Reserved words ko identifiers ke taur par use nahi karna chahiye.

### Example

```text
student
_student
@name
student1
```

---

# ⚠️ Important Point

SQL ke reserved words ko table ya column name ke taur par use karna avoid karna chahiye.

Example:

```text
SELECT
INSERT
CREATE
DELETE
```

Ye SQL ke keywords hain.

---

# 🟢 11. Square Brackets [ ]

SQL syntax mein:

```text
[ ]
```

ka matlab hota hai:

> Optional

Yani jo cheez `[ ]` ke andar ho usko likhna zaroori nahi.

### Example

```sql
SELECT [ALL | DISTINCT]
```

Iska matlab:

Aap `ALL` ya `DISTINCT` use kar sakte hain.

---

# 🟢 12. Curly Braces { }

Curly braces:

```text
{ }
```

ka matlab:

> Required item

Yani jo cheez braces mein hai woh dena zaroori hai.

### Example

```sql
FROM {table | view}
```

Yani `table` ya `view` mein se koi valid option dena zaroori hai.

---

# 🟢 13. Pipe Symbol |

Pipe:

```text
|
```

ka matlab hai:

> OR / Choice

Example:

```text
ALL | DISTINCT
```

Matlab:

- ALL
**ya**
- DISTINCT

dono mein se aik choose hoga.

---

# 🟢 14. [,…..n] Ka Matlab

Syntax mein:

```text
[,…..n]
```

ka matlab hai:

> Multiple items comma se separate kiye ja sakte hain.

Example:

```text
column1, column2, column3
```

---

# 🟣 15. SELECT Statement

SELECT SQL ki sab se important commands mein se aik hai.

Iska kaam:

> Database se data retrieve karna.

---

## Basic Syntax

```sql
SELECT column_name
FROM table_name;
```

---

## Sab Columns Select Karna

```sql
SELECT *
FROM student;
```

### `*` Ka Matlab

```text
* = All Columns
```

Yani student table ke tamam columns show honge.

---

# 🟣 16. SELECT Ki Lecture Syntax

Lecture mein syntax:

```sql
SELECT [ALL|DISTINCT]
{*|select_list}
FROM {table|view[,…n]}
```

Ab isko simple tarike se samajhte hain.

### SELECT

Data retrieve karne ke liye.

### ALL

Sab values ko return karne ke liye.

### DISTINCT

Duplicate values ko remove karne ke liye.

### `*`

All columns.

### select_list

Specific columns.

### FROM

Data kis table ya view se lena hai.

---

# 🟣 17. SELECT Example

```sql
SELECT *
FROM student;
```

Meaning:

> Student table ke tamam columns aur tamam records show karo.

---

## Specific Columns

Agar sirf student ka naam aur CGPA chahiye:

```sql
SELECT stName, cgpa
FROM student;
```

Is mein sirf:

- `stName`
- `cgpa`

show honge.

---

# 🟣 18. DISTINCT

`DISTINCT` duplicate values ko remove karta hai.

Example:

Agar table mein programs:

```text
BSSE
BSCS
BSSE
BBA
BSSE
```

hain aur hum likhein:

```sql
SELECT DISTINCT prName
FROM student;
```

Result:

```text
BSSE
BSCS
BBA
```

Yani repeated `BSSE` sirf aik dafa show hoga.

---

# 🟠 19. SQL Server Data Types

Database ke har column ka aik data type hota hai.

Data type batata hai:

> Is column mein kis type ka data store ho sakta hai?

Examples:

```text
INT       → Whole Number
VARCHAR   → Text
DECIMAL   → Decimal Number
DATE      → Date
BIT       → 0 or 1
```

---

# 🔢 20. Integer Data Types

Integer ka matlab:

> Whole Number

Examples:

```text
10
25
100
5000
-10
```

Decimal numbers:

```text
10.5
25.75
```

integers nahi hain.

---

# 🔢 21. BIGINT

`BIGINT` bohat large whole numbers ke liye use hota hai.

Lecture ke mutabiq range:

```text
-9,223,372,036,854,775,808
to
 9,223,372,036,854,775,807
```

Example:

```sql
population BIGINT
```

---

# 🔢 22. INT

`INT` common integer values ke liye use hota hai.

Range:

```text
-2,147,483,648
to
 2,147,483,647
```

Example:

```sql
stId INT
```

Student ID ke liye `INT` use kiya ja sakta hai.

---

# 🔢 23. SMALLINT

`SMALLINT` comparatively chhote integer values ke liye.

Range:

```text
-32,768
to
32,767
```

Example:

```sql
semester SMALLINT
```

---

# 🔢 24. TINYINT

`TINYINT` ki range:

```text
0 to 255
```

Example:

```sql
age TINYINT
```

---

# ☑️ 25. BIT

`BIT` sirf:

```text
0
1
```

store karta hai.

Isko simple taur par:

```text
0 = No / False
1 = Yes / True
```

samajh sakte hain.

### Example

```sql
isActive BIT
```

Agar student active hai:

```text
1
```

warna:

```text
0
```

---

# 🔢 26. DECIMAL

`DECIMAL` fixed precision aur scale wali numeric values ke liye use hota hai.

Example:

```sql
salary DECIMAL(10,2)
```

Ye decimal values ke liye useful hai.

Examples:

```text
50000.50
1250.75
999.99
```

---

# 🔢 27. NUMERIC

`NUMERIC` functionally `DECIMAL` ke equivalent hai.

Example:

```sql
cgpa NUMERIC(3,2)
```

Possible values:

```text
3.25
3.50
3.75
4.00
```

---

# 📝 28. Text Data Types

Text data types words, names, addresses aur doosri textual information ko store karte hain.

Important types:

```text
CHAR
VARCHAR
TEXT
NCHAR
NVARCHAR
NTEXT
```

---

# 📝 29. CHAR

`CHAR` fixed-length text ke liye use hota hai.

Lecture ke mutabiq default 30 characters aur maximum 8000 characters tak.

Example:

```sql
gender CHAR(1)
```

Values:

```text
M
F
```

---

# 📝 30. VARCHAR

`VARCHAR` variable-length text ke liye use hota hai.

Lecture ke mutabiq maximum 8000 characters.

Example:

```sql
stName VARCHAR(50)
```

Agar naam:

```text
Ali
```

hai to sirf required text length ko handle karta hai rather than fixed 50-character field concept.

---

# 📝 31. TEXT

`TEXT` variable-length textual data ko handle karta hai.

Ye long text ke liye historically use hota raha hai.

---

# 📝 32. NCHAR

`NCHAR` fixed-length Unicode character data ke liye use hota hai.

---

# 📝 33. NVARCHAR

`NVARCHAR` variable-length Unicode text ke liye.

Example:

```sql
studentName NVARCHAR(100)
```

---

# 📝 34. NTEXT

`NTEXT` Unicode text data ke liye.

---

# 💰 35. Money Data Types

Money values yani paisa/salary/price waghera ke liye money data types use kiye ja sakte hain.

Important types:

```text
SMALLMONEY
MONEY
```

---

# 💰 36. SMALLMONEY

Lecture ke mutabiq:

- 6 digits
- 4 decimal places

Example:

```sql
price SMALLMONEY
```

---

# 💰 37. MONEY

Lecture ke mutabiq:

- 15 digits
- 4 decimal places

Example:

```sql
salary MONEY
```

---

# 🌊 38. Floating Point Data Types

Floating-point types decimal/fractional numeric values ke liye use hote hain.

Important:

```text
FLOAT
REAL
```

Examples:

```text
3.14
12.50
99.99
```

---

# 📅 39. Date Data Types

Dates aur date/time information ke liye:

```text
SMALLDATETIME
DATETIME
```

use kiye jate hain.

Example:

```sql
birthDate DATETIME
```

---

# 🟢 40. Relational Database Design

Lecture mein conceptual database design ko relational database design mein convert kiya gaya.

Relations/tables ye hain:

```text
PROGRAM
COURSE
SEMESTER
CROFRD
FACULTY
STUDENT
ENROLL
SEM_RES
```

---

# 🗂️ 41. PROGRAM Table

```text
PROGRAM (prName, totSem, prCredits)
```

### Columns

| Column | Meaning |
|---|---|
| prName | Program Name |
| totSem | Total Semesters |
| prCredits | Total Program Credits |

### Example

```text
BS Software Engineering | 8 | 135
```

---

# 🗂️ 42. COURSE Table

```text
COURSE (crCode, crName, crCredits, prName)
```

| Column | Meaning |
|---|---|
| crCode | Course Code |
| crName | Course Name |
| crCredits | Course Credits |
| prName | Program Name |

### Example

```text
CS403 | Database Management Systems | 3 | BSSE
```

---

# 🗂️ 43. SEMESTER Table

```text
SEMESTER (semName, stDate, endDate)
```

| Column | Meaning |
|---|---|
| semName | Semester Name |
| stDate | Start Date |
| endDate | End Date |

### Example

```text
Spring 2026 | 01-02-2026 | 30-06-2026
```

---

# 🗂️ 44. CROFRD Table

```text
CROFRD (crCode, semName, facId)
```

| Column | Meaning |
|---|---|
| crCode | Course Code |
| semName | Semester Name |
| facId | Faculty ID |

Ye table course, semester aur faculty ke darmiyan relation ko represent karti hai.

---

# 🗂️ 45. FACULTY Table

```text
FACULTY (facId, fName, fQual, fSal, rank)
```

| Column | Meaning |
|---|---|
| facId | Faculty ID |
| fName | Faculty Name |
| fQual | Faculty Qualification |
| fSal | Faculty Salary |
| rank | Faculty Rank |

### Example

```text
F101 | Ahmed | PhD | 150000 | Professor
```

---

# 🗂️ 46. STUDENT Table

```text
STUDENT (
    stId,
    stName,
    stFName,
    stAdres,
    stPhone,
    prName,
    curSem,
    cgpa
)
```

| Column | Meaning |
|---|---|
| stId | Student ID |
| stName | Student Name |
| stFName | Father Name |
| stAdres | Address |
| stPhone | Phone Number |
| prName | Program Name |
| curSem | Current Semester |
| cgpa | CGPA |

### Example

```text
101 | Ali | Ahmed | Karachi | 03001234567 | BSSE | 4 | 3.50
```

---

# 🗂️ 47. ENROLL Table

```text
ENROLL (
    stId,
    crCode,
    semName,
    mTerm,
    sMrks,
    fMrks,
    totMrks,
    grade,
    gp
)
```

Ye table student ke course enrollment aur marks ko store karti hai.

| Column | Meaning |
|---|---|
| stId | Student ID |
| crCode | Course Code |
| semName | Semester |
| mTerm | Mid Term Marks |
| sMrks | Sessional Marks |
| fMrks | Final Marks |
| totMrks | Total Marks |
| grade | Grade |
| gp | Grade Point |

### Example

```text
101 | CS403 | Spring 2026 | 20 | 25 | 40 | 85 | A | 4.0
```

---

# 🗂️ 48. SEM_RES Table

```text
SEM_RES (
    stId,
    semName,
    totCrs,
    totCrdts,
    totGP,
    gpa
)
```

Ye semester ka summarized result store karti hai.

| Column | Meaning |
|---|---|
| stId | Student ID |
| semName | Semester |
| totCrs | Total Courses |
| totCrdts | Total Credits |
| totGP | Total Grade Points |
| gpa | Semester GPA |

### Example

```text
101 | Spring 2026 | 5 | 15 | 52.5 | 3.50
```

---

# 🟣 49. Data Dictionary

DDL statements compile hone ke baad database ki information ek special file/storage mein rakhi jati hai jise:

**Data Dictionary**
ya
**Data Directory**

kaha jata hai.

---

# 🧠 50. Metadata Kya Hai?

Metadata ka matlab:

> **Data about Data**

Yani data ke baare mein information.

### Example

Suppose:

```sql
stId INT
stName VARCHAR(50)
cgpa DECIMAL(3,2)
```

Actual data:

```text
101
Ali
3.50
```

Lekin:

```text
stId = INT
stName = VARCHAR(50)
cgpa = DECIMAL(3,2)
```

ye metadata hai.

### Easy Difference

```text
Data     → Ali
Metadata → Ali ka data kis column mein aur kis type mein store hota hai
```

---

# 🟢 51. Data Storage and Definition Language

Database ke:

- storage structure
- access methods

ko define karne ke liye DDL ki special type ka zikr lecture mein kiya gaya hai jise:

**Data Storage and Definition Language**

kaha gaya hai.

---

# 🟢 52. DML Ka Purpose

DML ka main purpose database mein stored information ko access aur manipulate karna hai.

DML se hum:

```text
Retrieve
Insert
Delete
Modify
```

kar sakte hain.

---

# 🟠 53. Procedural DML

Procedural DML mein user specify karta hai:

1. **What data is needed**
2. **How to get that data**

Yani:

```text
What + How
```

### Simple Example

User keh raha hai:

> Mujhe students ka data chahiye aur pehle student table ko scan karo, phir condition apply karo.

Yahan user process/method bhi define kar raha hai.

---

# 🟠 54. Non-Procedural DML

Non-Procedural DML mein user sirf batata hai:

> Mujhe konsa data chahiye.

Yani:

```text
Only What
```

Database system khud decide karta hai ke data kaise retrieve karna hai.

### SQL ka Important Concept

SQL generally non-procedural nature ko represent karti hai.

Aap result batate hain, database system retrieval ka method choose karta hai.

---

# 🔐 55. Access Control Commands

SQL mein kuch commands database aur data tak access control karne ke liye use hoti hain.

Important commands:

```text
GRANT
REVOKE
```

---

# 🔐 56. GRANT

`GRANT` ka matlab hai:

> Permission dena.

Example:

```sql
GRANT SELECT ON student TO user1;
```

Meaning:

> `user1` ko student table se data dekhne ki permission do.

---

# 🔐 57. REVOKE

`REVOKE` ka matlab hai:

> Di hui permission ko wapas lena.

Example:

```sql
REVOKE SELECT ON student FROM user1;
```

Meaning:

> `user1` se student table ki SELECT permission wapas lo.

---

# 🌍 58. SQL As A Standard Language

SQL relational database systems ke liye standard language ke taur par use hoti hai.

Lecture mein **ANSI** ka zikr hai.

## ANSI

**American National Standards Institute**

SQL ko relational database management systems ke liye standard language ke context mein mention kiya gaya hai.

---

# 🌐 59. SQL Use Karne Wale Systems

Lecture mein kuch examples:

- Oracle
- Sybase
- Microsoft SQL Server
- Microsoft Access
- Ingres

In systems mein SQL use hoti hai.

---

# ⚠️ 60. SQL Standard Aur Proprietary Extensions

Different database systems standard SQL commands ko support karte hain.

Lekin kuch systems apni **additional proprietary features/extensions** bhi provide karte hain.

Yani:

```text
Common SQL
+
DBMS Specific Features
```

Isi wajah se aik DBMS mein kuch extra syntax ho sakta hai jo doosre DBMS mein exactly same na ho.

---

# ⭐ 61. Most Important SQL Commands

## SELECT

Data retrieve karna.

```sql
SELECT * FROM student;
```

---

## INSERT

Naya record add karna.

```sql
INSERT INTO student
VALUES (101, 'Ali');
```

---

## UPDATE

Existing record ko modify karna.

```sql
UPDATE student
SET stName = 'Ahmed'
WHERE stId = 101;
```

---

## DELETE

Record delete karna.

```sql
DELETE FROM student
WHERE stId = 101;
```

---

## CREATE

Naya object/table create karna.

```sql
CREATE TABLE student (
    stId INT,
    stName VARCHAR(50)
);
```

---

## DROP

Table/object remove karna.

```sql
DROP TABLE student;
```

---

# 🟣 62. SELECT vs INSERT vs UPDATE vs DELETE

| Command | Kaam |
|---|---|
| SELECT | Data dekhna |
| INSERT | Naya data add karna |
| UPDATE | Existing data change karna |
| DELETE | Data remove karna |

### Easy Example

Socho student table hai.

```text
SELECT → Students ko dekhna
INSERT → Naya student add karna
UPDATE → Student ka naam change karna
DELETE → Student ka record remove karna
```

---

# 🧠 63. DDL vs DML vs Access Control

| Category | Purpose | Examples |
|---|---|---|
| DDL | Structure define karna | CREATE, DROP |
| DML | Data manipulate karna | SELECT, INSERT, UPDATE, DELETE |
| Access Control | Permissions manage karna | GRANT, REVOKE |

### Easy Memory Trick

```text
DDL → Design
DML → Data
GRANT/REVOKE → Permission
```

---

# 📝 64. SQL Syntax Symbols – Quick Revision

| Symbol | Meaning |
|---|---|
| `[ ]` | Optional |
| `{ }` | Required |
| `|` | OR / Choice |
| `*` | All columns |
| `[,…..n]` | Multiple comma-separated items |

---

# 🧠 65. Data Types – Quick Revision

| Data Type | Use |
|---|---|
| BIGINT | Very large integer |
| INT | Normal integer |
| SMALLINT | Small integer |
| TINYINT | 0 to 255 |
| BIT | 0 or 1 |
| DECIMAL | Exact decimal numbers |
| NUMERIC | Decimal/numeric values |
| CHAR | Fixed-length text |
| VARCHAR | Variable-length text |
| TEXT | Variable-length text |
| NCHAR | Unicode fixed-length text |
| NVARCHAR | Unicode variable-length text |
| NTEXT | Unicode text |
| SMALLMONEY | Money values |
| MONEY | Money values |
| FLOAT | Floating-point number |
| REAL | Floating-point number |
| SMALLDATETIME | Date and time |
| DATETIME | Date and time |

---

# 🎯 66. Exam Important Questions

## Q1. SQL kya hai?

SQL (Structured Query Language) aik language hai jo relational databases ke saath communicate karne aur data ko retrieve, insert, update, delete aur manage karne ke liye use hoti hai.

---

## Q2. DDL kya hai?

DDL ka full form **Data Definition Language** hai.

Ye database ki structure define karne ke liye use hoti hai.

Examples:

```text
CREATE
DROP
```

---

## Q3. DML kya hai?

DML ka full form **Data Manipulation Language** hai.

Ye database mein stored data ko retrieve, insert, modify aur delete karne ke liye use hoti hai.

Examples:

```text
SELECT
INSERT
UPDATE
DELETE
```

---

## Q4. Procedural aur Non-Procedural DML mein difference?

### Procedural

User specify karta hai:

```text
What + How
```

### Non-Procedural

User specify karta hai:

```text
Only What
```

---

## Q5. Metadata kya hai?

Metadata ka matlab:

> **Data about Data**

Yani data ki characteristics aur structure ke baare mein information.

---

## Q6. Data Dictionary kya hota hai?

Data Dictionary aik special storage hai jahan database ke metadata ke baare mein information store hoti hai.

---

## Q7. SELECT ka kya kaam hai?

Database se data retrieve karna.

Example:

```sql
SELECT * FROM student;
```

---

## Q8. INSERT ka kya kaam hai?

Database mein naya record insert/add karna.

---

## Q9. UPDATE ka kya kaam hai?

Existing record ki values ko modify/change karna.

---

## Q10. DELETE ka kya kaam hai?

Table se records remove karna.

---

## Q11. CREATE ka kya kaam hai?

Database objects jaise tables create karna.

---

## Q12. DROP ka kya kaam hai?

Database object jaise table ko remove karna.

---

## Q13. GRANT kya karta hai?

User ko permission/access deta hai.

---

## Q14. REVOKE kya karta hai?

Previously given permission ko wapas leta hai.

---

## Q15. `*` ka kya matlab hai?

`*` ka matlab:

> **All Columns**

---

# 🧩 67. Complete Example

Suppose hum `student` table create karna chahte hain.

## Step 1 – Table Create

```sql
CREATE TABLE student (
    stId INT,
    stName VARCHAR(50),
    stPhone VARCHAR(20),
    cgpa DECIMAL(3,2)
);
```

---

## Step 2 – Data Insert

```sql
INSERT INTO student
VALUES (101, 'Ali', '03001234567', 3.50);
```

---

## Step 3 – Data Read

```sql
SELECT *
FROM student;
```

---

## Step 4 – Specific Columns Read

```sql
SELECT stName, cgpa
FROM student;
```

---

## Step 5 – Data Update

```sql
UPDATE student
SET cgpa = 3.75
WHERE stId = 101;
```

---

## Step 6 – Data Delete

```sql
DELETE FROM student
WHERE stId = 101;
```

---

## Step 7 – Table Drop

```sql
DROP TABLE student;
```

---

# ⚠️ 68. CREATE Aur INSERT Ka Difference

Ye bohat important difference hai.

### CREATE

Structure banata hai.

```sql
CREATE TABLE student (...);
```

### INSERT

Structure ke andar data add karta hai.

```sql
INSERT INTO student VALUES (...);
```

### Easy Example

```text
CREATE  → Ghar banao
INSERT  → Ghar mein saman rakho
```

---

# ⚠️ 69. DROP Aur DELETE Ka Difference

Ye bhi exam mein important ho sakta hai.

### DELETE

Table ke **records/data** ko delete karta hai.

Example:

```sql
DELETE FROM student;
```

Table structure rehti hai.

### DROP

Table ko hi remove kar deta hai.

Example:

```sql
DROP TABLE student;
```

### Easy Difference

```text
DELETE → Data remove
DROP   → Table remove
```

---

# ⚠️ 70. DELETE Aur UPDATE Mein Difference

### DELETE

Data remove karta hai.

```sql
DELETE FROM student
WHERE stId = 101;
```

### UPDATE

Data change karta hai.

```sql
UPDATE student
SET cgpa = 3.80
WHERE stId = 101;
```

---

# 🧠 71. Real Life Example

Socho University ka database hai.

Us mein `student` table hai:

| stId | stName | program | cgpa |
|---|---|---|---:|
| 101 | Ali | BSSE | 3.50 |
| 102 | Sara | BSCS | 3.80 |
| 103 | Ahmed | BSSE | 3.20 |

### Sab students dekhna:

```sql
SELECT * FROM student;
```

### Sirf names dekhna:

```sql
SELECT stName FROM student;
```

### Naya student add karna:

```sql
INSERT INTO student
VALUES (104, 'Hina', 'BSSE', 3.60);
```

### CGPA change karna:

```sql
UPDATE student
SET cgpa = 3.90
WHERE stId = 102;
```

### Student delete karna:

```sql
DELETE FROM student
WHERE stId = 103;
```

---

# ⭐ 72. Lecture Ka Most Important Concept

Is lecture ka core idea ye hai:

```text
SQL
│
├── Database se communicate karti hai
│
├── DDL
│   ├── CREATE
│   └── DROP
│
├── DML
│   ├── SELECT
│   ├── INSERT
│   ├── UPDATE
│   └── DELETE
│
└── Access Control
    ├── GRANT
    └── REVOKE
```

---

# 📌 73. One-Page Revision

## SQL

**Structured Query Language**

Database ke saath communicate karne ke liye use hoti hai.

---

## DDL

**Data Definition Language**

Structure define karti hai.

```text
CREATE
DROP
```

---

## DML

**Data Manipulation Language**

Data ke saath kaam karti hai.

```text
SELECT
INSERT
UPDATE
DELETE
```

---

## Access Control

```text
GRANT
REVOKE
```

---

## SQL Syntax

```text
[ ]       → Optional
{ }       → Required
|         → OR / Choice
*         → All Columns
[,…..n]   → Multiple items
```

---

## Metadata

```text
Metadata = Data about Data
```

---

## Important Data Types

```text
BIGINT
INT
SMALLINT
TINYINT
BIT

DECIMAL
NUMERIC

CHAR
VARCHAR
TEXT
NCHAR
NVARCHAR
NTEXT

SMALLMONEY
MONEY

FLOAT
REAL

SMALLDATETIME
DATETIME
```

---

# 📝 74. Practice Exercise

Neeche diye commands ki practice karein.

## Table Create Karein

```sql
CREATE TABLE student (
    stId INT,
    stName VARCHAR(50),
    cgpa DECIMAL(3,2)
);
```

## Record Insert Karein

```sql
INSERT INTO student
VALUES (101, 'Ali', 3.50);
```

## Record Dekhein

```sql
SELECT * FROM student;
```

## Record Update Karein

```sql
UPDATE student
SET cgpa = 3.75
WHERE stId = 101;
```

## Record Delete Karein

```sql
DELETE FROM student
WHERE stId = 101;
```

---

# ✅ 75. Final Summary

Lecture 25 mein humne **SQL (Structured Query Language)** ke basics parhe.

SQL database ke saath communication ke liye use hoti hai.

Humne seekha ke:

- SQL database se data retrieve kar sakti hai.
- SQL data insert kar sakti hai.
- SQL data update kar sakti hai.
- SQL data delete kar sakti hai.
- SQL database objects create kar sakti hai.
- SQL database objects drop kar sakti hai.
- DDL database structure define karti hai.
- DML database ke data ko manipulate karti hai.
- Procedural DML mein user batata hai **what + how**.
- Non-Procedural DML mein user sirf **what** batata hai.
- `GRANT` permission dene ke liye use hota hai.
- `REVOKE` permission wapas lene ke liye use hota hai.
- Data Dictionary metadata store karta hai.
- Metadata ka matlab **Data about Data** hai.
- SQL mein different data types use hote hain jaise INT, VARCHAR, DECIMAL, DATE etc.
- SELECT statement data retrieve karne ke liye bohat important hai.

---

# 🎯 Final Easy Memory Trick

```text
DDL  → Database ki Structure
DML  → Database ka Data
DCL/Access → Database ki Permission
```

Aur commands ko yun yaad rakhein:

```text
SELECT  → Dekho
INSERT  → Add Karo
UPDATE  → Change Karo
DELETE  → Delete Karo

CREATE  → Banao
DROP    → Hatao

GRANT   → Permission Do
REVOKE  → Permission Wapas Lo
```

# ⭐ Golden Rule

```text
DDL = Structure
DML = Data
GRANT/REVOKE = Access
```

**Ye Lecture 25 ke sab se important concepts hain aur exam preparation ke liye inhein zaroor revise karein.**
```
