# 📚 DBMS – Lecture 28
## INSERT Statement, SELECT Statement, Alias, Expressions, DISTINCT & WHERE

> **Course:** Database Management System (CS403)  
> **Lecture:** 28  
> **Topic:** Data Manipulation Language (DML)  
> **Language:** Roman Urdu + English SQL Terms

---

# 📌 Lecture Overview

Is lecture mein hum **Data Manipulation Language (DML)** ke important SQL commands aur concepts parhenge:

1. `INSERT` Statement
2. `VALUES` Clause
3. Column List
4. `SELECT` Statement
5. `SELECT *`
6. Specific Columns Select Karna
7. Column Alias
8. Expressions in `SELECT`
9. `DISTINCT` Keyword
10. `WHERE` Clause
11. Predicate
12. `TRUE`, `FALSE`, aur `UNKNOWN`
13. Column-to-Column Comparison

---

# 1. DML Kya Hai?

**DML = Data Manipulation Language**

DML SQL commands ka woh group hai jo database ke andar موجود data ko **add, retrieve, modify, ya delete** karne ke liye use hota hai.

Is lecture mein mainly:

- `INSERT` → new data add karna
- `SELECT` → existing data retrieve/read karna

par focus hai.

---

# 2. INSERT Statement

## INSERT Kya Hai?

`INSERT` statement ka use kisi existing table mein **new record/row add** karne ke liye hota hai.

Simple words mein:

> **INSERT ka matlab hai table ke andar naya data dalna.**

### Real-Life Example

Socho university ke paas `STUDENT` table hai:

| stId | stName | prName | cgpa |
|---|---|---|---:|
| S1020 | Sohail Dar | MCS | 2.80 |
| S1038 | Shoaib Ali | BCS | 2.78 |

Ab ek naya student admission leta hai:

- ID = S1040
- Name = Ali Raza
- Program = BSSE
- CGPA = 3.20

To humein new row insert karni hogi.

```sql
INSERT INTO student
VALUES ('S1040', 'Ali Raza', 'BSSE', 3.20);
```

---

# 3. INSERT ke Do Basic Forms

SQL mein `INSERT` ke do common forms hain.

## Form 1: VALUES ke Saath

```sql
INSERT INTO table_name [(column_list)]
VALUES (value_list);
```

Is form mein hum directly values provide karte hain.

### Example

```sql
INSERT INTO course
VALUES ('CS-211', 'Operating Systems', 4, 'MCS');
```

---

## Form 2: Query ke Result se Insert

```sql
INSERT INTO table_name [(column_list)]
(query_specification);
```

Is form mein kisi `SELECT` query ka result use karke ek ya multiple rows insert ki ja sakti hain.

### Example

```sql
INSERT INTO old_students (stId, stName)
SELECT stId, stName
FROM student
WHERE cgpa >= 3.0;
```

### Is query ka matlab

`student` table se woh students select karo jinka CGPA 3.0 ya us se zyada hai aur unka ID/name `old_students` mein insert kar do.

> **Note:** Target aur source columns ke data types compatible hone chahiye.

---

# 4. Column List Kya Hoti Hai?

INSERT ke andar hum specify kar sakte hain ke kin columns mein values insert karni hain.

### Syntax

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

### Example

```sql
INSERT INTO course (crCode, crName)
VALUES ('CS-316', 'Database Systems');
```

Yahan humne sirf:

- `crCode`
- `crName`

mein values di hain.

Baaki columns ko value nahi di gayi.

Agar baaki columns `NULL` allow karte hain, to unmein `NULL` store ho sakta hai.

---

# 5. Column List Na Dein To Kya Hoga?

Agar hum INSERT ke waqt column names nahi dete:

```sql
INSERT INTO course
VALUES ('CS-211', 'Operating Systems', 4, 'MCS');
```

to values table ke **default column order** mein insert hoti hain.

Agar table:

```text
COURSE
--------------------------------------------
crCode | crName | crCredits | prName
```

to values ka order bhi yahi hona chahiye:

```text
1. crCode
2. crName
3. crCredits
4. prName
```

### ⚠️ Important

Agar order galat ho gaya to wrong data insert ho sakta hai ya data type error aa sakta hai.

---

# 6. VALUES Clause

`VALUES` clause new row ki values provide karta hai.

### General Syntax

```sql
VALUES (value1, value2, ...);
```

Values mein ho sakti hain:

- Literal values
- Expressions
- `NULL`

### Example

```sql
INSERT INTO course
VALUES ('CS-211', 'Operating Systems', 4, 'MCS');
```

Yahan:

- `'CS-211'` → String
- `'Operating Systems'` → String
- `4` → Number
- `'MCS'` → String

---

# 7. INSERT mein NULL

Agar kisi column ke paas data available nahi hai, aur column `NULL` allow karta hai, to hum `NULL` use kar sakte hain.

### Example

```sql
INSERT INTO course
VALUES ('MG-103', 'Intro to Management', NULL, NULL);
```

Table mein result:

| crCode | crName | crCredits | prName |
|---|---|---:|---|
| MG-103 | Intro to Management | NULL | NULL |

### NULL ka Matlab

`NULL` ka matlab hota hai:

> **Value unknown hai ya currently available nahi hai.**

`NULL` ko `0` ya empty string samajhna ghalat hai.

---

# 8. INSERT Values ki Important Conditions

`VALUES` mein values ki quantity selected columns ke count ke barabar honi chahiye.

### Correct

```sql
INSERT INTO course (crCode, crName)
VALUES ('CS-316', 'Database Systems');
```

2 columns → 2 values ✅

### Incorrect

```sql
INSERT INTO course (crCode, crName)
VALUES ('CS-316');
```

2 columns → 1 value ❌

---

# 9. Data Type Match

Inserted value ka data type corresponding column ke data type ke compatible hona chahiye.

Example:

```text
crCredits → INTEGER
```

To:

```sql
INSERT INTO course
VALUES ('CS-211', 'Operating Systems', 4, 'MCS');
```

mein `4` number hai, is liye correct hai.

Lekin:

```sql
INSERT INTO course
VALUES ('CS-211', 'Operating Systems', 'Four', 'MCS');
```

problem create kar sakta hai agar `crCredits` numeric column hai.

---

# 10. Complete COURSE Example

Hum ek sample `COURSE` table assume karte hain:

```sql
CREATE TABLE course (
    crCode VARCHAR(10),
    crName VARCHAR(100),
    crCredits INT,
    prName VARCHAR(50)
);
```

Ab kuch records insert karte hain:

```sql
INSERT INTO course
VALUES ('CS-211', 'Operating Systems', 4, 'MCS');

INSERT INTO course
VALUES ('CS-316', 'Database Systems', 3, 'BSSE');

INSERT INTO course
VALUES ('MG-103', 'Intro to Management', NULL, NULL);
```

Table:

| crCode | crName | crCredits | prName |
|---|---|---:|---|
| CS-211 | Operating Systems | 4 | MCS |
| CS-316 | Database Systems | 3 | BSSE |
| MG-103 | Intro to Management | NULL | NULL |

---

# 11. SELECT Statement

## SELECT Kya Hai?

`SELECT` SQL ka bohat important command hai.

Is ka use database se **data retrieve/read** karne ke liye hota hai.

Simple words:

> **SELECT ka matlab hai database se required data nikalna.**

### Real-Life Example

Agar teacher ko sirf students ke names chahiye:

```sql
SELECT stName
FROM student;
```

Agar teacher ko complete student record chahiye:

```sql
SELECT *
FROM student;
```

---

# 12. SELECT ki Basic Clauses

Basic SELECT statement mein 3 important clauses hoti hain:

```text
SELECT
FROM
WHERE
```

Inka simple meaning:

| Clause | Kaam |
|---|---|
| SELECT | Kaun se columns chahiye? |
| FROM | Kis table se chahiye? |
| WHERE | Kaun si rows chahiye? |

### Basic Structure

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

> `WHERE` optional hai.

---

# 13. SELECT * – Saare Columns

Asterisk `*` ka matlab hota hai:

> **Table ke tamam columns select karo.**

### Example

```sql
SELECT *
FROM student;
```

Agar table mein columns hain:

```text
stId
stName
prName
cgpa
```

to `SELECT *` sab columns return karega.

### Result

| stId | stName | prName | cgpa |
|---|---|---|---:|
| S1020 | Sohail Dar | MCS | 2.8 |
| S1038 | Shoaib Ali | BCS | 2.78 |
| S1015 | Tahira Ejaz | MCS | 3.2 |
| S1034 | Sadia Zia | BIT | NULL |
| S1018 | Arif Zia | BIT | 3.0 |

---

# 14. Specific Columns Select Karna

Agar humein sirf kuch columns chahiye to unke names likhte hain.

### Example

```sql
SELECT stName, prName
FROM student;
```

Result:

| stName | prName |
|---|---|
| Sohail Dar | MCS |
| Shoaib Ali | BCS |
| Tahira Ejaz | MCS |
| Sadia Zia | BIT |
| Arif Zia | BIT |

### Important

`SELECT *` → all columns

`SELECT stName, prName` → only selected columns

---

# 15. SELECT mein Column Order Change Karna

SELECT mein columns jis order mein likhenge, output bhi usi order mein aayega.

Example:

```sql
SELECT prName, stName
FROM student;
```

Output:

| prName | stName |
|---|---|
| MCS | Sohail Dar |
| BCS | Shoaib Ali |
| MCS | Tahira Ejaz |
| BIT | Sadia Zia |
| BIT | Arif Zia |

Yani table ka actual structure change nahi hua, sirf query ka output order change hua.

---

# 16. Column Alias

## Alias Kya Hai?

Alias ka use column ko output mein **temporary/custom name** dene ke liye hota hai.

### Syntax

```sql
SELECT column_name AS alias_name
FROM table_name;
```

`AS` optional ho sakta hai.

### Example

```sql
SELECT stName AS 'Student Name'
FROM student;
```

Output mein:

```text
Student Name
```

show hoga, instead of `stName`.

---

# 17. Alias ki Real Example

```sql
SELECT
    stName AS 'Student Name',
    prName AS 'Program'
FROM student;
```

Result:

| Student Name | Program |
|---|---|
| Sohail Dar | MCS |
| Shoaib Ali | BCS |
| Tahira Ejaz | MCS |
| Sadia Zia | BIT |
| Arif Zia | BIT |

### Important

Alias **original table ka column name change nahi karta**.

Sirf query ke output mein naam change hota hai.

---

# 18. AS Optional Hai

Dono forms common hain:

```sql
SELECT stName AS 'Student Name'
FROM student;
```

Aur:

```sql
SELECT stName 'Student Name'
FROM student;
```

Lekin readability ke liye `AS` use karna beginners ke liye zyada clear hota hai.

---

# 19. SELECT mein Expressions

SELECT clause mein hum calculation bhi perform kar sakte hain.

Example:

```sql
SELECT mTerm + sMrks
FROM enroll;
```

Har row ke liye calculation hogi.

Agar:

```text
mTerm = 20
sMrks = 18
```

to:

```text
20 + 18 = 38
```

Output mein `38` milega.

---

# 20. Marks ki Real Example

Assume `enroll` table:

| stId | crCode | mTerm | sMrks |
|---|---|---:|---:|
| S1020 | CS101 | 20 | 18 |
| S1038 | CS101 | 22 | 19 |
| S1015 | CS101 | 25 | 20 |

Query:

```sql
SELECT
    stId,
    crCode,
    mTerm + sMrks AS 'Total out of 50'
FROM enroll;
```

Output:

| stId | crCode | Total out of 50 |
|---|---|---:|
| S1020 | CS101 | 38 |
| S1038 | CS101 | 41 |
| S1015 | CS101 | 45 |

### Important

Ye calculation table ke andar automatically save nahi hoti.

`SELECT` yahan **result calculate karke display** kar raha hai.

---

# 21. DISTINCT Keyword

## DISTINCT Kya Hai?

`DISTINCT` duplicate values ko remove karta hai.

### Syntax

```sql
SELECT DISTINCT column_name
FROM table_name;
```

---

# 22. DISTINCT ki Real Example

Student table:

| stId | stName | prName |
|---|---|---|
| S1020 | Sohail Dar | MCS |
| S1038 | Shoaib Ali | BCS |
| S1015 | Tahira Ejaz | MCS |
| S1034 | Sadia Zia | BIT |
| S1018 | Arif Zia | BIT |

Agar hum likhein:

```sql
SELECT prName
FROM student;
```

Result:

| prName |
|---|
| MCS |
| BCS |
| MCS |
| BIT |
| BIT |

Duplicate values bhi aa rahi hain.

Ab:

```sql
SELECT DISTINCT prName
FROM student;
```

Result logically:

| prName |
|---|
| MCS |
| BCS |
| BIT |

### Simple Rule

```text
SELECT      → duplicates aa sakte hain
DISTINCT    → duplicate values remove
```

---

# 23. DISTINCT Kab Use Karein?

DISTINCT useful hai jab humein:

- Unique programs
- Unique cities
- Unique departments
- Unique categories
- Unique course codes

chahiye hon.

### Example

```sql
SELECT DISTINCT prName
FROM student;
```

### Real World

Agar 500 employees hain lekin sirf unique departments dekhne hain:

```sql
SELECT DISTINCT department
FROM employees;
```

---

# 24. WHERE Clause

## WHERE Kya Hai?

`WHERE` clause rows ko **filter** karta hai.

Simple words:

> WHERE batata hai ke **kaunsi rows retrieve karni hain**.

### Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

---

# 25. WHERE ka Simple Example

Question:

> Sirf MCS ke students show karo.

```sql
SELECT *
FROM student
WHERE prName = 'MCS';
```

Result:

| stId | stName | prName | cgpa |
|---|---|---|---:|
| S1020 | Sohail Dar | MCS | 2.8 |
| S1015 | Tahira Ejaz | MCS | 3.2 |

---

# 26. WHERE ke Saath Different Conditions

## CGPA 3 Se Greater

```sql
SELECT *
FROM student
WHERE cgpa > 3.0;
```

## CGPA 3 Ke Barabar

```sql
SELECT *
FROM student
WHERE cgpa = 3.0;
```

## Program BCS

```sql
SELECT stName
FROM student
WHERE prName = 'BCS';
```

## Student ID Specific

```sql
SELECT *
FROM student
WHERE stId = 'S1020';
```

---

# 27. Comparison Operators

WHERE mein commonly ye operators use hote hain:

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `<>` | Not equal |
| `!=` | Not equal (DBMS support ke mutabiq) |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

### Examples

```sql
WHERE cgpa > 3.0
```

```sql
WHERE cgpa >= 3.0
```

```sql
WHERE cgpa < 3.0
```

```sql
WHERE prName = 'MCS'
```

---

# 28. Predicate Kya Hota Hai?

`WHERE` ke baad jo logical condition hoti hai usay **predicate** kehte hain.

Example:

```sql
WHERE prName = 'MCS'
```

Yahan:

```text
prName = 'MCS'
```

predicate hai.

Ye condition evaluate hoti hai aur result:

```text
TRUE
FALSE
UNKNOWN
```

ho sakta hai.

---

# 29. TRUE, FALSE, UNKNOWN

Suppose:

```sql
WHERE color = 'Red'
```

### Case 1 – TRUE

Agar:

```text
color = 'Red'
```

to result `TRUE`.

### Case 2 – FALSE

Agar:

```text
color = 'Blue'
```

to result `FALSE`.

### Case 3 – UNKNOWN

Agar:

```text
color = NULL
```

to comparison:

```sql
color = 'Red'
```

ka result `UNKNOWN` hota hai.

---

# 30. NULL ke Saath Important Point

`NULL` ko normal value ki tarah compare nahi karna chahiye.

Ye query:

```sql
SELECT *
FROM student
WHERE cgpa = NULL;
```

correct way nahi hai for checking NULL.

NULL check karne ke liye aam tor par:

```sql
SELECT *
FROM student
WHERE cgpa IS NULL;
```

use kiya jata hai.

Aur NULL na ho:

```sql
SELECT *
FROM student
WHERE cgpa IS NOT NULL;
```

> Ye NULL behavior samajhna bohat important hai.

---

# 31. Column-to-Column Comparison

SQL mein hum sirf column ko literal value se compare nahi karte.

Hum **do columns** ko bhi compare kar sakte hain.

### Example

```sql
SELECT *
FROM student
WHERE student.stId = enroll.stId;
```

Yahan:

```text
student.stId
```

aur:

```text
enroll.stId
```

do columns hain.

Ye concept **JOIN** operations mein bohat important hota hai.

---

# 32. Real-Life Database Example

Imagine ek university database mein do tables hain.

## STUDENT

| stId | stName | prName |
|---|---|---|
| S101 | Ali | BSSE |
| S102 | Sara | BCS |
| S103 | Hamza | MCS |

## ENROLL

| stId | crCode | marks |
|---|---|---:|
| S101 | CS101 | 45 |
| S102 | CS101 | 40 |
| S103 | CS101 | 48 |

Agar hum student aur enrollment records ko student ID ki basis par match karna chahte hain, to column-to-column comparison use hoti hai:

```sql
SELECT student.stName, enroll.crCode
FROM student, enroll
WHERE student.stId = enroll.stId;
```

Yahan:

```text
student.stId = enroll.stId
```

matching condition hai.

---

# 33. SELECT + WHERE + Alias Example

Ek query mein multiple concepts combine kiye ja sakte hain.

Question:

> MCS students ke names aur CGPA custom headings ke saath show karo.

```sql
SELECT
    stName AS 'Student Name',
    cgpa AS 'CGPA'
FROM student
WHERE prName = 'MCS';
```

Output:

| Student Name | CGPA |
|---|---:|
| Sohail Dar | 2.8 |
| Tahira Ejaz | 3.2 |

---

# 34. SELECT + DISTINCT + WHERE Example

Question:

> Sirf un unique programs ke names show karo jahan students ka CGPA 3.0 ya us se zyada hai.

```sql
SELECT DISTINCT prName
FROM student
WHERE cgpa >= 3.0;
```

Is query mein:

- `SELECT` → data retrieve karta hai
- `DISTINCT` → duplicate programs remove karta hai
- `FROM` → student table se data leta hai
- `WHERE` → CGPA ki condition lagata hai

---

# 35. INSERT vs SELECT

| Feature | INSERT | SELECT |
|---|---|---|
| Purpose | New data add karna | Data retrieve karna |
| Existing data read karta hai? | Direct purpose nahi | ✅ |
| New row add karta hai? | ✅ | ❌ |
| `VALUES` use hota hai? | ✅ Common form mein | ❌ |
| `WHERE` use ho sakta hai? | Kuch forms mein indirectly/query ke saath | ✅ |
| Example | `INSERT INTO...` | `SELECT...FROM...` |

---

# 36. SELECT Clause ka Easy Formula

Exam mein is formula ko yaad rakhein:

```text
SELECT  → KYA chahiye?
FROM    → KAHAAN se chahiye?
WHERE   → KIN rows ke liye chahiye?
```

### Example

```sql
SELECT stName
FROM student
WHERE cgpa > 3.0;
```

Is ka meaning:

> Student table se un students ke names lao jinka CGPA 3.0 se zyada hai.

---

# 37. Important SQL Examples – Quick Revision

## All Data

```sql
SELECT *
FROM student;
```

## Specific Columns

```sql
SELECT stName, prName
FROM student;
```

## Alias

```sql
SELECT stName AS 'Student Name'
FROM student;
```

## Expression

```sql
SELECT mTerm + sMrks AS 'Total'
FROM enroll;
```

## Distinct Values

```sql
SELECT DISTINCT prName
FROM student;
```

## Filter by Program

```sql
SELECT *
FROM student
WHERE prName = 'MCS';
```

## Filter by CGPA

```sql
SELECT stName
FROM student
WHERE cgpa >= 3.0;
```

## NULL Check

```sql
SELECT *
FROM student
WHERE cgpa IS NULL;
```

## Insert Complete Row

```sql
INSERT INTO student
VALUES ('S1040', 'Ali Raza', 'BSSE', 3.2);
```

## Insert Specific Columns

```sql
INSERT INTO course (crCode, crName)
VALUES ('CS-316', 'Database Systems');
```

---

# 38. Common Mistakes

## Mistake 1 – INSERT mein Values ka Wrong Order

❌ Wrong:

```sql
INSERT INTO course
VALUES ('Operating Systems', 'CS-211', 'MCS', 4);
```

Agar table order:

```text
crCode, crName, crCredits, prName
```

hai to order same hona chahiye.

---

## Mistake 2 – Columns se Zyada Values

❌ Wrong:

```sql
INSERT INTO course (crCode, crName)
VALUES ('CS-316', 'Database Systems', 3);
```

2 columns ke liye 3 values di gayi hain.

✅ Correct:

```sql
INSERT INTO course (crCode, crName)
VALUES ('CS-316', 'Database Systems');
```

---

## Mistake 3 – `SELECT *` ka Excessive Use

Development aur learning mein `SELECT *` useful hai.

Lekin real systems mein agar sirf kuch columns chahiye hon to specific columns select karna zyada clear aur efficient hota hai.

Example:

```sql
SELECT stName, cgpa
FROM student;
```

---

## Mistake 4 – NULL ko `=` se Compare Karna

❌ Avoid:

```sql
WHERE cgpa = NULL
```

✅ Use:

```sql
WHERE cgpa IS NULL
```

---

## Mistake 5 – String ke Quotes Bhool Jana

❌ Wrong:

```sql
WHERE prName = MCS
```

✅ Correct:

```sql
WHERE prName = 'MCS'
```

---

# 39. Exam Important Questions

### Q1. INSERT statement kya karti hai?

**Answer:** `INSERT` statement existing table mein new row/record add karti hai.

---

### Q2. INSERT ke do forms kya hain?

**Answer:**

```sql
INSERT INTO table_name [(column_list)]
VALUES (value_list);
```

aur:

```sql
INSERT INTO table_name [(column_list)]
(query_specification);
```

---

### Q3. SELECT statement ka purpose kya hai?

**Answer:** Database tables se required data retrieve karna.

---

### Q4. `*` ka kya matlab hai?

**Answer:** Table ke tamam columns select karna.

---

### Q5. WHERE clause kis liye use hoti hai?

**Answer:** Rows ko condition ki basis par filter karne ke liye.

---

### Q6. DISTINCT kis liye use hota hai?

**Answer:** Duplicate values ko remove karke unique values return karne ke liye.

---

### Q7. Alias kya hota hai?

**Answer:** Output mein column ko temporary/custom name dena.

---

### Q8. Predicate kya hota hai?

**Answer:** WHERE clause ki logical condition ko predicate kehte hain, jo TRUE, FALSE ya UNKNOWN evaluate ho sakti hai.

---

# 40. One-Minute Revision

```text
INSERT
↓
New data add karta hai

SELECT
↓
Data retrieve karta hai

*
↓
All columns

Specific column names
↓
Sirf required columns

AS
↓
Column alias/custom heading

Expression
↓
Calculation in SELECT

DISTINCT
↓
Duplicate values remove

WHERE
↓
Rows filter

Predicate
↓
Logical condition

TRUE / FALSE / UNKNOWN
↓
Predicate ke possible results
```

---

# 41. Complete Mini Practice Database

Neeche ek small practice example hai jo aap MySQL/SQL Server jaise DBMS environment mein concepts samajhne ke liye use kar sakte hain. SQL dialect ke mutabiq small syntax differences ho sakti hain.

## Step 1 – Student Table

```sql
CREATE TABLE student (
    stId VARCHAR(10),
    stName VARCHAR(100),
    prName VARCHAR(50),
    cgpa DECIMAL(3,2)
);
```

## Step 2 – Data Insert Karein

```sql
INSERT INTO student
VALUES ('S1020', 'Sohail Dar', 'MCS', 2.80);

INSERT INTO student
VALUES ('S1038', 'Shoaib Ali', 'BCS', 2.78);

INSERT INTO student
VALUES ('S1015', 'Tahira Ejaz', 'MCS', 3.20);

INSERT INTO student
VALUES ('S1034', 'Sadia Zia', 'BIT', NULL);

INSERT INTO student
VALUES ('S1018', 'Arif Zia', 'BIT', 3.00);
```

## Step 3 – Sab Students Dekhein

```sql
SELECT *
FROM student;
```

## Step 4 – Sirf Names Dekhein

```sql
SELECT stName
FROM student;
```

## Step 5 – Names + Program Dekhein

```sql
SELECT stName, prName
FROM student;
```

## Step 6 – Custom Headings

```sql
SELECT
    stName AS 'Student Name',
    prName AS 'Program'
FROM student;
```

## Step 7 – Unique Programs

```sql
SELECT DISTINCT prName
FROM student;
```

## Step 8 – MCS Students

```sql
SELECT *
FROM student
WHERE prName = 'MCS';
```

## Step 9 – CGPA 3 or More

```sql
SELECT stName, cgpa
FROM student
WHERE cgpa >= 3.0;
```

## Step 10 – NULL CGPA

```sql
SELECT *
FROM student
WHERE cgpa IS NULL;
```

---

# 42. Final Summary

Is lecture mein humne SQL ke do bohat important DML concepts deeply samjhe:

## INSERT

`INSERT` ke through hum database table mein **new records add** karte hain.

```sql
INSERT INTO student
VALUES ('S1040', 'Ali Raza', 'BSSE', 3.20);
```

## SELECT

`SELECT` ke through hum database se **required data retrieve** karte hain.

```sql
SELECT stName, prName
FROM student;
```

## Alias

```sql
SELECT stName AS 'Student Name'
FROM student;
```

## Expression

```sql
SELECT mTerm + sMrks AS 'Total'
FROM enroll;
```

## DISTINCT

```sql
SELECT DISTINCT prName
FROM student;
```

## WHERE

```sql
SELECT *
FROM student
WHERE prName = 'MCS';
```

### Golden Rule

```text
INSERT  → Data andar dalo
SELECT  → Data bahar nikalo
WHERE   → Data filter karo
DISTINCT → Duplicate hatao
AS      → Naam/change heading do
*       → Sab columns lao
```

---

# 📝 Practice Questions

## Basic

1. `INSERT` statement kya hoti hai?
2. `VALUES` clause ka purpose kya hai?
3. Column-list kis liye use hoti hai?
4. `SELECT *` aur `SELECT column_name` mein kya difference hai?
5. Alias kya hota hai?
6. `DISTINCT` kyun use karte hain?
7. `WHERE` clause kya karti hai?
8. Predicate kya hota hai?
9. Predicate ke three possible results kya hain?
10. `NULL` ko check karne ka correct syntax kya hai?

## SQL Practice

### Q1. Student ke sirf names show karein.

```sql
SELECT stName
FROM student;
```

### Q2. MCS students show karein.

```sql
SELECT *
FROM student
WHERE prName = 'MCS';
```

### Q3. Unique programs show karein.

```sql
SELECT DISTINCT prName
FROM student;
```

### Q4. CGPA 3.0 ya zyada students show karein.

```sql
SELECT stName, cgpa
FROM student
WHERE cgpa >= 3.0;
```

### Q5. New student insert karein.

```sql
INSERT INTO student
VALUES ('S1041', 'Ayesha Khan', 'BSSE', 3.50);
```

---

# ✅ Lecture 28 Complete

**Main concepts to remember:**

```text
INSERT
VALUES
Column List
SELECT
FROM
WHERE
Alias
Expressions
DISTINCT
Predicate
TRUE / FALSE / UNKNOWN
NULL
Column-to-Column Comparison
```

> **Best learning method:** Har query ko sirf read na karein. Khud SQL editor mein run karein aur output observe karein. Is se `SELECT`, `WHERE`, `DISTINCT` aur `INSERT` ka concept bohat jaldi clear ho jayega.
