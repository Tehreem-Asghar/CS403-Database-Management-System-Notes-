# 📚 DBMS – Lecture 27
## ALTER TABLE, DELETE, TRUNCATE, DROP & Data Manipulation Language (DML)

---

## 📖 Lecture Overview

Previous lecture mein hum ne **DDL (Data Definition Language)** aur `CREATE TABLE` command parhi thi.

Is lecture mein hum existing tables ko modify karna aur database ke data ke sath kaam karna seekhenge.

### Is lecture ke important topics:

1. ALTER TABLE
2. ADD COLUMN
3. ALTER COLUMN
4. DROP COLUMN
5. RENAME COLUMN
6. Add/Drop Constraints
7. TRUNCATE TABLE
8. DELETE
9. DROP TABLE
10. Data Manipulation Language (DML)
11. Procedural vs Non-Procedural Language
12. INSERT
13. SELECT
14. UPDATE
15. DELETE
16. INSERT...VALUES
17. INSERT...SELECT
18. Important Differences
19. Real-Life Examples
20. Practice Exercise

---

# 1. ALTER TABLE

## 🔹 ALTER TABLE Kya Hai?

`ALTER TABLE` ka use kisi **already existing table ke structure/design mein changes** karne ke liye hota hai.

Yani agar hum ne pehle table create kar li hai aur baad mein us mein koi change karna ho, to `ALTER TABLE` use karte hain.

### Simple Definition:

> **ALTER TABLE = Existing table ke structure mein modification karna.**

---

## 🔹 ALTER TABLE se Hum Kya Kar Sakte Hain?

Hum existing table mein:

- Naya column add kar sakte hain
- Existing column modify kar sakte hain
- Column delete kar sakte hain
- Column ka naam change kar sakte hain
- Constraint add kar sakte hain
- Constraint remove kar sakte hain
- Default value change kar sakte hain

---

# 2. Basic ALTER TABLE Syntax

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

Ya:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

Ya:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

Ya:

```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

---

# 3. ALTER TABLE ke Important Parts

| Part | Meaning |
|---|---|
| `table_name` | Jis table ko change karna hai |
| `column_name` | Jis column ko add/modify/delete karna hai |
| `new_name` | Column ka naya naam |
| `datatype` | Column ka data type |
| `size` | Data ki size |
| `DEFAULT` | Default value |

---

# 4. ADD COLUMN

## 🔹 ADD COLUMN Kya Hai?

`ADD COLUMN` ka use existing table mein **new column add karne** ke liye hota hai.

### Syntax:

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

---

## 🔹 Example

Maan lein hamare paas `Student` table hai:

```text
Student
-------------------------
RollNo
Name
Age
```

Ab humein `City` column add karna hai.

```sql
ALTER TABLE Student
ADD City VARCHAR(30);
```

Ab table:

```text
Student
-------------------------
RollNo
Name
Age
City
```

---

# 5. ADD COLUMN with DEFAULT

Hum new column ke sath default value bhi de sakte hain.

```sql
ALTER TABLE Student
ADD City VARCHAR(30) DEFAULT 'Karachi';
```

Ab agar kisi student ki city explicitly provide nahi ki gayi, to default value:

```text
Karachi
```

use ho sakti hai.

### Real-Life Example

University ke students ke table mein hum city add karna chahte hain:

```sql
ALTER TABLE Student
ADD City VARCHAR(30) DEFAULT 'Karachi';
```

---

# 6. ALTER COLUMN

## 🔹 ALTER COLUMN Kya Hai?

`ALTER COLUMN` ka use existing column ko modify karne ke liye hota hai.

Hum column ka:

- Data type
- Size
- Default value

change kar sakte hain.

### Syntax:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

---

## 🔹 Example

Suppose:

```text
stFName CHAR(10)
```

Ab humein is ki size 20 karni hai:

```sql
ALTER TABLE Student
ALTER COLUMN stFName CHAR(20);
```

Ab `stFName` ki size 20 characters ho gayi.

---

# 7. DROP COLUMN

## 🔹 DROP COLUMN Kya Hai?

`DROP COLUMN` ka use existing table se **ek column remove/delete** karne ke liye hota hai.

### Syntax:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

---

## 🔹 Example

Suppose `Student` table:

| RollNo | Name | Age | CurSem |
|---|---|---:|---:|
| 101 | Ali | 20 | 4 |
| 102 | Sara | 21 | 5 |

Agar humein `CurSem` column ki zarurat nahi:

```sql
ALTER TABLE Student
DROP COLUMN CurSem;
```

Ab table:

| RollNo | Name | Age |
|---|---|---:|
| 101 | Ali | 20 |
| 102 | Sara | 21 |

### ⚠️ Important:

Column drop karne se us column ka stored data bhi remove ho jata hai.

---

# 8. RENAME COLUMN

## 🔹 RENAME COLUMN Kya Hai?

`RENAME COLUMN` ka use column ka **naam change karne** ke liye hota hai.

### Syntax:

```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

---

## 🔹 Example

Pehle:

```text
stFName
```

Tha.

Hum naam change karna chahte hain:

```text
studentFirstName
```

To:

```sql
ALTER TABLE Student
RENAME COLUMN stFName TO studentFirstName;
```

Ab column ka naam `studentFirstName` ho jayega.

> **Note:** Exact `ALTER TABLE` syntax DBMS ke mutabiq thora different ho sakta hai. Apne course ke DBMS syntax ko follow karein.

---

# 9. Constraint Add Karna

Existing table mein hum constraint bhi add kar sakte hain.

### Example:

```sql
ALTER TABLE Student
ADD CONSTRAINT fk_st_pr
FOREIGN KEY (prName)
REFERENCES Program(prName);
```

---

## 🔹 Is Command ko Samjhein

```sql
ALTER TABLE Student
```

Matlab `Student` table ko modify karo.

```sql
ADD CONSTRAINT fk_st_pr
```

Ek constraint add karo jiska naam `fk_st_pr` hai.

```sql
FOREIGN KEY (prName)
```

`prName` ko foreign key banao.

```sql
REFERENCES Program(prName);
```

Aur `Program` table ke `prName` ko reference karo.

---

# 10. Constraint ka Naam Kyun Dete Hain?

Constraint ka meaningful naam dena useful hota hai.

Example:

```text
fk_st_pr
```

Yahan:

- `fk` = Foreign Key
- `st` = Student
- `pr` = Program

Agar future mein humein is constraint ko remove karna ho:

```sql
ALTER TABLE Student
DROP CONSTRAINT fk_st_pr;
```

Is liye meaningful name dena useful hota hai.

---

# 11. DROP CONSTRAINT

## 🔹 DROP CONSTRAINT Kya Hai?

Existing table se constraint remove karne ke liye:

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

### Example:

```sql
ALTER TABLE Student
DROP CONSTRAINT ck_st_pr;
```

Is se `ck_st_pr` constraint remove ho jayega.

---

# 12. ALTER TABLE ke Complete Examples

### New column add:

```sql
ALTER TABLE Student
ADD Age INT;
```

### Existing column modify:

```sql
ALTER TABLE Student
ALTER COLUMN stFName CHAR(20);
```

### Column remove:

```sql
ALTER TABLE Student
DROP COLUMN CurSem;
```

### Column rename:

```sql
ALTER TABLE Student
RENAME COLUMN stFName TO FirstName;
```

### Constraint add:

```sql
ALTER TABLE Student
ADD CONSTRAINT fk_st_pr
FOREIGN KEY (prName)
REFERENCES Program(prName);
```

### Constraint remove:

```sql
ALTER TABLE Student
DROP CONSTRAINT fk_st_pr;
```

---

# 13. TRUNCATE TABLE

## 🔹 TRUNCATE Kya Hai?

`TRUNCATE TABLE` ka use table ki **saari rows delete/remove** karne ke liye hota hai.

### Syntax:

```sql
TRUNCATE TABLE table_name;
```

### Example:

```sql
TRUNCATE TABLE Student;
```

Is command ke baad:

- Student table rahegi
- Table ka structure rahega
- Columns rahenge
- Lekin existing rows remove ho jayengi

---

# 14. TRUNCATE ka Real Example

Before:

| RollNo | Name | Age |
|---:|---|---:|
| 101 | Ali | 20 |
| 102 | Sara | 21 |
| 103 | Ahmed | 22 |

Command:

```sql
TRUNCATE TABLE Student;
```

After:

| RollNo | Name | Age |
|---|---|---|
| *(No rows)* | | |

Lekin `Student` table ab bhi exist karti hai.

---

# 15. DELETE

## 🔹 DELETE Kya Hai?

`DELETE` ka use table se **one ya multiple records remove** karne ke liye hota hai.

### Syntax:

```sql
DELETE FROM table_name
WHERE condition;
```

---

## 🔹 Example

Sirf RollNo 101 wale student ko delete karna:

```sql
DELETE FROM Student
WHERE RollNo = 101;
```

Sirf woh record delete hoga jiska RollNo `101` hai.

---

# 16. DELETE with Multiple Rows

Hum condition ke through multiple rows bhi delete kar sakte hain.

Example:

```sql
DELETE FROM Student
WHERE Age < 18;
```

Is se un tamam students ke records delete honge jinki age 18 se kam hai.

---

# 17. DELETE Without WHERE

Agar hum `WHERE` condition na lagayen:

```sql
DELETE FROM Student;
```

To table ki **saari rows delete** ho jayengi.

### Lekin:

```text
Table       → Rahegi
Structure   → Rahega
Rows        → Delete
```

---

# 18. DROP TABLE

## 🔹 DROP TABLE Kya Hai?

`DROP TABLE` ka use **complete table ko database se remove** karne ke liye hota hai.

### Syntax:

```sql
DROP TABLE table_name;
```

### Example:

```sql
DROP TABLE Student;
```

Is se:

- Table delete
- Table ka structure delete
- Table ka data delete

sab kuch remove ho jata hai.

---

# 19. TRUNCATE vs DELETE vs DROP

Ye exam ke liye bohat important difference hai.

| Command | Rows Delete | Table Structure | Table Exist |
|---|---|---|---|
| `DELETE` | Selected/All rows | Rehti hai | ✅ Yes |
| `TRUNCATE` | All rows | Rehta hai | ✅ Yes |
| `DROP TABLE` | All data | Delete ho jata hai | ❌ No |

---

## 🔹 Simple Formula

```text
DELETE   → Rows delete
TRUNCATE → All rows delete
DROP     → Entire table delete
```

---

# 20. Real-Life Example of DELETE, TRUNCATE and DROP

Maan lein school database mein:

```text
Student
------------------
101  Ali
102  Ahmed
103  Sara
```

### Sirf Ali ko delete karna:

```sql
DELETE FROM Student
WHERE RollNo = 101;
```

Result:

```text
102 Ahmed
103 Sara
```

---

### Saare students ko delete karna:

```sql
TRUNCATE TABLE Student;
```

Result:

```text
Student table remains
All rows removed
```

---

### Puri Student table hi remove karna:

```sql
DROP TABLE Student;
```

Result:

```text
Student table does not exist anymore
```

---

# 21. Data Manipulation Language (DML)

## 🔹 DML Kya Hai?

DML ka full form hai:

> **Data Manipulation Language**

DML ka use database ke **data ko manipulate** karne ke liye hota hai.

Yani hum:

- Data add karte hain
- Data read karte hain
- Data change karte hain
- Data delete karte hain

---

# 22. DML ke Basic Commands

| DML Command | Purpose |
|---|---|
| `INSERT` | New data add karna |
| `SELECT` | Data retrieve/read karna |
| `UPDATE` | Existing data change karna |
| `DELETE` | Data remove karna |

---

# 23. DML ko Real Life se Samjhein

Suppose ek university ke paas `Student` table hai.

Agar new student admission le:

```text
INSERT
```

Agar student ka record dekhna hai:

```text
SELECT
```

Agar student ki information change karni hai:

```text
UPDATE
```

Agar student ka record remove karna hai:

```text
DELETE
```

### Easy Memory Trick

```text
INSERT  = ADD
SELECT  = READ
UPDATE  = CHANGE
DELETE  = REMOVE
```

---

# 24. SQL is Non-Procedural

SQL ki ek important characteristic yeh hai ke SQL ek **non-procedural language** hai.

Is ka matlab hai:

> User sirf yeh batata hai ke us ko **kya data chahiye**, database khud decide karta hai ke data **kaise retrieve** karna hai.

---

# 25. Procedural Language

Procedural language mein user ko specify karna hota hai:

1. Kya data chahiye
2. Data kaise retrieve karna hai
3. Kis process ko follow karna hai

Examples:

- C
- Pascal
- COBOL
- Modula-2

---

# 26. Non-Procedural Language

Non-procedural language mein user sirf batata hai:

> Mujhe konsa data chahiye?

Database Management System khud decide karta hai ke data ko kaise find karna hai.

### SQL

SQL ek **non-procedural language** hai.

---

# 27. Procedural vs Non-Procedural

| Procedural | Non-Procedural |
|---|---|
| What + How | Mostly What |
| User process specify karta hai | DBMS process decide karta hai |
| More implementation detail | Less implementation detail |
| C, Pascal etc. | SQL |

---

# 28. INSERT Command

## 🔹 INSERT Kya Hai?

`INSERT` command existing table mein **new row/record add** karne ke liye use hoti hai.

### Basic Syntax:

```sql
INSERT INTO table_name
(column1, column2, column3)
VALUES
(value1, value2, value3);
```

---

# 29. INSERT ka Simple Example

Suppose table:

```text
Student
--------------------------------
RollNo | Name | Age
```

New student add karna hai:

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20);
```

Result:

| RollNo | Name | Age |
|---:|---|---:|
| 101 | Ali | 20 |

---

# 30. INSERT with Multiple Rows

Agar SQL system multiple rows allow kare to:

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20),
(102, 'Sara', 21),
(103, 'Ahmed', 22);
```

Result:

| RollNo | Name | Age |
|---:|---|---:|
| 101 | Ali | 20 |
| 102 | Sara | 21 |
| 103 | Ahmed | 22 |

---

# 31. INSERT ke Important Rules

Data insert karte waqt kuch important rules follow karne hote hain.

### Rule 1: Data Type Correct Hona Chahiye

Agar column:

```sql
Age INT
```

hai to integer value deni chahiye:

```sql
INSERT INTO Student(Age)
VALUES (20);
```

Wrong example:

```sql
INSERT INTO Student(Age)
VALUES ('Hello');
```

`Hello` integer nahi hai, is liye error aa sakta hai.

---

# 32. Rule 2: Data ki Size Column se Match Karni Chahiye

Suppose:

```sql
Name CHAR(20)
```

Is ka matlab hai name ke liye limited size available hai.

Agar bohat lambi string insert karenge to error ya truncation ho sakti hai, database system ke behavior par depend karta hai.

### Correct:

```sql
INSERT INTO Student(Name)
VALUES ('Ali');
```

### Problematic example:

```sql
INSERT INTO Student(Name)
VALUES ('This is a very very long student name...');
```

Agar value column ki allowed size se exceed kare to issue aa sakta hai.

---

# 33. Rule 3: Values ka Order Correct Hona Chahiye

Suppose:

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20);
```

Mapping:

```text
RollNo → 101
Name   → Ali
Age    → 20
```

Yani:

```text
First value  → First column
Second value → Second column
Third value  → Third column
```

---

# 34. INSERT with NULL

Agar column `NULL` allow karta ho to hum `NULL` insert kar sakte hain.

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', NULL);
```

Yahan age ki value unknown/not provided hai.

### Important:

`NULL` ka matlab `0` nahi hota.

```text
NULL ≠ 0
NULL ≠ ''
```

`NULL` generally means value unknown/not available/not provided.

---

# 35. INSERT with DEFAULT

Agar column ki default value defined ho:

```sql
CREATE TABLE Student
(
    RollNo INT,
    Name VARCHAR(50),
    City VARCHAR(30) DEFAULT 'Karachi'
);
```

To:

```sql
INSERT INTO Student
(RollNo, Name)
VALUES
(101, 'Ali');
```

City automatically default value le sakti hai:

```text
Karachi
```

---

# 36. INSERT...VALUES

`INSERT...VALUES` ka use values provide karke record insert karne ke liye hota hai.

### Example:

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20);
```

---

# 37. INSERT...SELECT

`INSERT...SELECT` ka use ek table se data select karke doosri table mein insert karne ke liye hota hai.

### Example:

Suppose:

```text
Student
-------------------
RollNo | Name | Age
101    | Ali  | 20
102    | Sara | 21
```

Aur ek doosri table hai:

```text
NewStudent
```

Hum `Student` ka data `NewStudent` mein copy karna chahte hain:

```sql
INSERT INTO NewStudent
SELECT *
FROM Student;
```

---

# 38. INSERT...SELECT ka Real-Life Example

Maan lein university ne purane students ko archive karna hai.

Original table:

```text
Student
```

Archive table:

```text
Student_Archive
```

Data copy karne ke liye:

```sql
INSERT INTO Student_Archive
SELECT *
FROM Student;
```

Is tarah existing records doosri table mein insert ho jayenge.

---

# 39. SELECT Command

## 🔹 SELECT Kya Hai?

`SELECT` ka use database se data **retrieve/read/view** karne ke liye hota hai.

### Example:

```sql
SELECT *
FROM Student;
```

Is ka matlab:

> Student table ke tamam columns aur rows show karo.

---

# 40. SELECT Specific Columns

```sql
SELECT Name, Age
FROM Student;
```

Ab sirf:

- Name
- Age

show honge.

---

# 41. UPDATE Command

## 🔹 UPDATE Kya Hai?

`UPDATE` ka use existing records ke data ko **modify/change** karne ke liye hota hai.

### Syntax:

```sql
UPDATE table_name
SET column_name = new_value
WHERE condition;
```

---

# 42. UPDATE ka Example

Suppose:

| RollNo | Name | Age |
|---:|---|---:|
| 101 | Ali | 20 |

Ali ki age 21 karni hai:

```sql
UPDATE Student
SET Age = 21
WHERE RollNo = 101;
```

Result:

| RollNo | Name | Age |
|---:|---|---:|
| 101 | Ali | 21 |

---

# 43. UPDATE Multiple Columns

Hum ek hi command mein multiple columns bhi update kar sakte hain.

```sql
UPDATE Student
SET
    Name = 'Ali Ahmed',
    Age = 21
WHERE RollNo = 101;
```

---

# 44. UPDATE Without WHERE

⚠️ Bohat important:

Agar `UPDATE` mein `WHERE` condition na lagayen:

```sql
UPDATE Student
SET Age = 20;
```

To **table ke tamam students ki age 20** ho sakti hai.

Is liye real databases mein `UPDATE` ke sath `WHERE` carefully use karna chahiye.

---

# 45. DELETE Command

`DELETE` ka use existing table se records remove karne ke liye hota hai.

### Example:

```sql
DELETE FROM Student
WHERE RollNo = 101;
```

Is se RollNo 101 wala student delete hoga.

---

# 46. DELETE Multiple Rows

```sql
DELETE FROM Student
WHERE Age < 18;
```

Is se 18 se kam age wale tamam records delete ho sakte hain.

---

# 47. DELETE Without WHERE

```sql
DELETE FROM Student;
```

Is se table ke **saare records delete** ho jayenge.

Lekin:

```text
Table remains
Structure remains
Rows removed
```

---

# 48. Four Main DML Commands

```text
             DML
              |
    -------------------------
    |       |       |       |
 INSERT   SELECT  UPDATE  DELETE
    |       |       |       |
   Add     Read   Change  Remove
```

### Easy Trick:

> **I-S-U-D**

```text
I = Insert
S = Select
U = Update
D = Delete
```

---

# 49. ALTER vs INSERT

### ALTER:

Structure change karta hai.

```sql
ALTER TABLE Student
ADD City VARCHAR(30);
```

### INSERT:

Data add karta hai.

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20);
```

### Difference:

```text
ALTER  → Table ka structure
INSERT → Table ka data
```

---

# 50. ALTER vs UPDATE

### ALTER:

Column/table structure change:

```sql
ALTER TABLE Student
ADD City VARCHAR(30);
```

### UPDATE:

Existing row ki value change:

```sql
UPDATE Student
SET City = 'Lahore'
WHERE RollNo = 101;
```

### Difference:

```text
ALTER  → Structure modify
UPDATE → Data modify
```

---

# 51. DELETE vs TRUNCATE

| DELETE | TRUNCATE |
|---|---|
| Rows remove karta hai | All rows remove karta hai |
| `WHERE` use kar sakte hain | Condition-based row selection nahi |
| Specific records delete kar sakte hain | Entire table data clear karta hai |
| Table rehti hai | Table rehti hai |

### Example:

```sql
DELETE FROM Student
WHERE RollNo = 101;
```

Sirf selected record.

```sql
TRUNCATE TABLE Student;
```

Saare records.

---

# 52. DELETE vs DROP

| DELETE | DROP |
|---|---|
| Rows delete | Complete table delete |
| Table remains | Table removed |
| Structure remains | Structure removed |
| `WHERE` possible | `WHERE` nahi hota |

### Example:

```sql
DELETE FROM Student;
```

Table exists.

```sql
DROP TABLE Student;
```

Table no longer exists.

---

# 53. TRUNCATE vs DROP

| TRUNCATE | DROP |
|---|---|
| All rows remove | Entire table remove |
| Table structure remains | Structure removed |
| Table remains | Table removed |

### Easy Formula:

```text
TRUNCATE → Empty Table
DROP     → Remove Table
```

---

# 54. DDL vs DML

Ye bhi exam mein important hota hai.

## DDL

DDL ka full form:

> **Data Definition Language**

DDL database/table ki **structure define/change** karti hai.

Examples:

```text
CREATE
ALTER
DROP
TRUNCATE
```

---

## DML

DML ka full form:

> **Data Manipulation Language**

DML table ke **data** ko manipulate karti hai.

Examples:

```text
INSERT
SELECT
UPDATE
DELETE
```

---

# 55. DDL vs DML Table

| DDL | DML |
|---|---|
| Structure ke liye | Data ke liye |
| CREATE | INSERT |
| ALTER | SELECT |
| DROP | UPDATE |
| TRUNCATE | DELETE |

### Easy Trick:

```text
DDL → Design / Definition
DML → Data Manipulation
```

---

# 56. Complete Real-Life Student Database Example

## Step 1: Table Create

```sql
CREATE TABLE Student
(
    RollNo INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT,
    City VARCHAR(30)
);
```

---

## Step 2: Data Insert

```sql
INSERT INTO Student
(RollNo, Name, Age, City)
VALUES
(101, 'Ali', 20, 'Karachi');

INSERT INTO Student
(RollNo, Name, Age, City)
VALUES
(102, 'Sara', 21, 'Lahore');

INSERT INTO Student
(RollNo, Name, Age, City)
VALUES
(103, 'Ahmed', 22, 'Islamabad');
```

---

## Step 3: Data View

```sql
SELECT *
FROM Student;
```

Result:

| RollNo | Name | Age | City |
|---:|---|---:|---|
| 101 | Ali | 20 | Karachi |
| 102 | Sara | 21 | Lahore |
| 103 | Ahmed | 22 | Islamabad |

---

## Step 4: New Column Add

University ko students ka semester bhi store karna hai:

```sql
ALTER TABLE Student
ADD Semester INT;
```

---

## Step 5: Data Update

Ali ka semester 4 hai:

```sql
UPDATE Student
SET Semester = 4
WHERE RollNo = 101;
```

---

## Step 6: Sara ka City Change

```sql
UPDATE Student
SET City = 'Karachi'
WHERE RollNo = 102;
```

---

## Step 7: Student Delete

Agar RollNo 103 wala student record remove karna ho:

```sql
DELETE FROM Student
WHERE RollNo = 103;
```

---

## Step 8: Table Empty Karna

Agar table ka tamam data remove karna ho:

```sql
TRUNCATE TABLE Student;
```

Table rahegi lekin rows nahi hongi.

---

## Step 9: Complete Table Delete

Agar Student table ki zarurat hi nahi:

```sql
DROP TABLE Student;
```

Ab complete table remove ho jayegi.

---

# 57. INSERT mein Common Mistakes

## ❌ Mistake 1: Wrong Data Type

```sql
INSERT INTO Student(Age)
VALUES ('ABC');
```

Agar `Age` integer hai to issue hoga.

### ✅ Correct:

```sql
INSERT INTO Student(Age)
VALUES (20);
```

---

## ❌ Mistake 2: Wrong Column Order

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
('Ali', 101, 20);
```

Yahan values ka order columns se match nahi kar raha.

### ✅ Correct:

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20);
```

---

## ❌ Mistake 3: Column Size Exceed Karna

Agar:

```sql
Name VARCHAR(20)
```

hai aur bohat lambi string insert ki jaye to error/truncation ho sakti hai.

---

# 58. UPDATE mein Common Mistake

### ❌ Dangerous:

```sql
UPDATE Student
SET Age = 20;
```

Agar intention sirf ek student update karna tha to `WHERE` missing hai.

### ✅ Better:

```sql
UPDATE Student
SET Age = 20
WHERE RollNo = 101;
```

---

# 59. DELETE mein Common Mistake

### ❌ Dangerous:

```sql
DELETE FROM Student;
```

Ye saare records delete kar dega.

### ✅ Specific record:

```sql
DELETE FROM Student
WHERE RollNo = 101;
```

---

# 60. Exam Important Questions

### Q1. ALTER TABLE kya hota hai?

`ALTER TABLE` existing table ke structure mein changes karne ke liye use hota hai.

### Q2. ALTER TABLE se kya changes kiye ja sakte hain?

- Column add
- Column modify
- Column delete
- Column rename
- Constraint add/remove

### Q3. DELETE aur TRUNCATE mein difference?

`DELETE` selected ya all rows delete kar sakta hai, jab ke `TRUNCATE` table ki tamam rows ko remove karta hai aur table structure ko rakhta hai.

### Q4. DELETE aur DROP mein difference?

`DELETE` records delete karta hai, lekin table rehti hai.

`DROP TABLE` complete table ko database se remove karta hai.

### Q5. DML kya hai?

DML ka full form **Data Manipulation Language** hai. Is ka use database ke data ko insert, retrieve, update aur delete karne ke liye hota hai.

### Q6. DML ke basic commands kaun si hain?

```text
INSERT
SELECT
UPDATE
DELETE
```

### Q7. INSERT ka purpose kya hai?

Existing table mein new record add karna.

### Q8. SELECT kya karta hai?

Table se data retrieve/read karta hai.

### Q9. UPDATE kya karta hai?

Existing records ki values modify karta hai.

### Q10. DELETE kya karta hai?

Table se records remove karta hai.

### Q11. SQL procedural hai ya non-procedural?

SQL ko generally **non-procedural language** kaha jata hai.

---

# 61. Quick Revision Table

| Command | Purpose | Example |
|---|---|---|
| `ALTER` | Structure modify | `ALTER TABLE Student ADD City VARCHAR(30);` |
| `INSERT` | Data add | `INSERT INTO Student VALUES (...);` |
| `SELECT` | Data read | `SELECT * FROM Student;` |
| `UPDATE` | Data modify | `UPDATE Student SET Age=21 WHERE RollNo=101;` |
| `DELETE` | Rows remove | `DELETE FROM Student WHERE RollNo=101;` |
| `TRUNCATE` | All rows remove | `TRUNCATE TABLE Student;` |
| `DROP` | Table remove | `DROP TABLE Student;` |

---

# 62. One-Line Memory Notes

```text
ALTER TABLE
→ Existing table ka structure change karta hai.

ADD COLUMN
→ New column add karta hai.

ALTER COLUMN
→ Existing column modify karta hai.

DROP COLUMN
→ Column remove karta hai.

RENAME COLUMN
→ Column ka naam change karta hai.

ADD CONSTRAINT
→ Constraint add karta hai.

DROP CONSTRAINT
→ Constraint remove karta hai.

INSERT
→ New row add karta hai.

SELECT
→ Data read karta hai.

UPDATE
→ Existing data change karta hai.

DELETE
→ Rows delete karta hai.

TRUNCATE
→ All rows delete karta hai, table rehti hai.

DROP TABLE
→ Complete table remove karta hai.
```

---

# 63. Final Concept Map

```text
                         SQL
                          |
             ---------------------------
             |                         |
            DDL                       DML
             |                         |
      ----------------          -----------------
      |      |      |          |      |      |   |
   CREATE  ALTER   DROP     INSERT SELECT UPDATE DELETE
                    |
                  TABLE

                  Other Important
                      Commands
                         |
                 ----------------
                 |              |
             TRUNCATE         DELETE
                 |
          All Rows Remove
          Table Remains
```

---

# 64. Final Summary

Lecture 27 mein hum ne SQL ke **ALTER TABLE** aur **Data Manipulation Language (DML)** ko detail mein study kiya.

### Sab se important concepts:

```text
ALTER
→ Existing table ka structure modify

INSERT
→ New data add

SELECT
→ Data retrieve

UPDATE
→ Existing data modify

DELETE
→ Specific/all rows remove

TRUNCATE
→ All rows remove, table remains

DROP TABLE
→ Complete table remove
```

### DDL:

```text
CREATE
ALTER
DROP
TRUNCATE
```

### DML:

```text
INSERT
SELECT
UPDATE
DELETE
```

### Most Important Difference:

```text
ALTER    → Structure Change
UPDATE   → Data Change

DELETE   → Rows Delete
TRUNCATE → All Rows Delete
DROP     → Complete Table Delete
```

---

# 📝 Practice Exercise

Neeche di gayi practice khud SQL mein run karein.

## Task 1 — Student Table Create

```sql
CREATE TABLE Student
(
    RollNo INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

## Task 2 — 3 Students Insert

```sql
INSERT INTO Student
(RollNo, Name, Age)
VALUES
(101, 'Ali', 20),
(102, 'Sara', 21),
(103, 'Ahmed', 22);
```

## Task 3 — Saare Students Display

```sql
SELECT *
FROM Student;
```

## Task 4 — City Column Add

```sql
ALTER TABLE Student
ADD City VARCHAR(30);
```

## Task 5 — Ali ki City Karachi Karein

```sql
UPDATE Student
SET City = 'Karachi'
WHERE RollNo = 101;
```

## Task 6 — RollNo 103 Delete Karein

```sql
DELETE FROM Student
WHERE RollNo = 103;
```

## Task 7 — Table ke Saare Records Remove Karein

```sql
TRUNCATE TABLE Student;
```

## Task 8 — Complete Table Remove Karein

```sql
DROP TABLE Student;
```

---

# 🎯 Final Exam Revision

> **ALTER = Table Structure Change**

> **INSERT = Add Data**

> **SELECT = Read Data**

> **UPDATE = Change Data**

> **DELETE = Remove Rows**

> **TRUNCATE = Remove All Rows**

> **DROP = Remove Complete Table**

> **DML = INSERT + SELECT + UPDATE + DELETE**

> **SQL = Non-Procedural Language**

---

## ⭐ Golden Rule

```text
ALTER → Structure
INSERT → Add
SELECT → Read
UPDATE → Change
DELETE → Remove Rows
TRUNCATE → Empty Table
DROP → Remove Table
```

---

## 📌 Note

SQL syntax mein kuch commands ka exact form DBMS (jaise MySQL, SQL Server, PostgreSQL, Oracle) ke mutabiq different ho sakta hai. Exam aur practical mein apne course ke specified DBMS syntax ko follow karein.
