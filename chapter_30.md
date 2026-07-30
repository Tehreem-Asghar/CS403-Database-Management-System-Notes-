# 📚 DBMS — Lecture 30
## SQL Functions, Aggregate Functions, GROUP BY, HAVING & Cartesian Product

> **Course:** CS403 — Database Management Systems  
> **Lecture:** 30  
> **Focus:** ORDER BY, SQL Functions, Aggregate Functions, GROUP BY, HAVING, Multiple Tables & Cartesian Product

---

# 📌 Lecture Overview

Is lecture mein hum SQL ke kuch bohat important concepts parhenge:

1. `ORDER BY` Clause
2. SQL Functions
3. Functions ki Categories
4. String Functions
5. Conversion Functions
6. Nested Functions
7. Aggregate Functions
8. `GROUP BY` Clause
9. `HAVING` Clause
10. `WHERE` vs `HAVING`
11. Multiple Tables se Data Access Karna
12. Cartesian Product

---

# 1. ORDER BY Clause

## 🔹 ORDER BY kya hai?

`ORDER BY` ka use query ke result ko **sort/order** karne ke liye hota hai.

Is sorting ko hum:

- Ascending order mein kar sakte hain
- Descending order mein kar sakte hain

### Syntax

```sql
SELECT column1, column2
FROM table_name
ORDER BY column_name ASC;
```

Ya:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column_name DESC;
```

### ASC aur DESC

| Keyword | Meaning | Example |
|---|---|---|
| `ASC` | Ascending | A → Z, 1 → 10 |
| `DESC` | Descending | Z → A, 10 → 1 |

Agar `ASC` ya `DESC` nahi likha jaye, to normally **ascending order** assume kiya jata hai.

---

## ✅ Real Example 1 — Student CGPA Sort Karna

### Student Table

| student_id | name | cgpa |
|---:|---|---:|
| 1 | Ali | 3.20 |
| 2 | Sara | 3.90 |
| 3 | Ahmed | 2.80 |
| 4 | Hina | 3.60 |

### Lowest se Highest CGPA

```sql
SELECT name, cgpa
FROM student
ORDER BY cgpa ASC;
```

### Result

| name | cgpa |
|---|---:|
| Ahmed | 2.80 |
| Ali | 3.20 |
| Hina | 3.60 |
| Sara | 3.90 |

### Highest se Lowest CGPA

```sql
SELECT name, cgpa
FROM student
ORDER BY cgpa DESC;
```

### Result

| name | cgpa |
|---|---:|
| Sara | 3.90 |
| Hina | 3.60 |
| Ali | 3.20 |
| Ahmed | 2.80 |

---

## ✅ Real Example 2 — IBM Suppliers

```sql
SELECT supplier_city
FROM supplier
WHERE supplier_name = 'IBM'
ORDER BY supplier_city;
```

Ye IBM ke suppliers ki cities ko ascending order mein show karega.

Descending:

```sql
SELECT supplier_city
FROM supplier
WHERE supplier_name = 'IBM'
ORDER BY supplier_city DESC;
```

---

# 2. SQL Functions

## 🔹 Function kya hota hai?

SQL mein function ek special operation hota hai jo input ko process karke **result/value return** karta hai.

Example:

```sql
SELECT UPPER('ali');
```

Result:

```text
ALI
```

Ek aur example:

```sql
SELECT LEN('Pakistan');
```

Result:

```text
8
```

---

# 3. Types of Functions

SQL functions ko generally do major types mein samjha ja sakta hai:

## 1. Built-in Functions

Ye functions database system pehle se provide karta hai.

Examples:

```text
AVG()
COUNT()
SUM()
UPPER()
LOWER()
LEN()
MAX()
MIN()
```

## 2. User-Defined Functions

Ye functions programmer/database developer khud define kar sakta hai.

---

# 4. Categories of SQL Functions

Lecture mein SQL Server ke context mein functions ki following categories di gayi hain:

| Category | Examples | Purpose |
|---|---|---|
| Mathematical | `ABS()`, `ROUND()`, `SIN()`, `SQRT()` | Mathematical calculations |
| String | `LOWER()`, `UPPER()`, `SUBSTRING()`, `LEN()` | Text processing |
| Date | `DATEDIFF()`, `DATEPART()`, `GETDATE()` | Date/time operations |
| System | `USER`, `DATALENGTH()`, `HOST_NAME()` | System information |
| Conversion | `CAST()`, `CONVERT()` | Data type conversion |

---

# 5. Mathematical Functions

Mathematical functions numbers par calculations karti hain.

## ABS()

Kisi number ki absolute value return karta hai.

```sql
SELECT ABS(-25);
```

Result:

```text
25
```

## ROUND()

Number ko round karta hai.

```sql
SELECT ROUND(15.678, 2);
```

Result:

```text
15.68
```

## SQRT()

Square root nikalta hai.

```sql
SELECT SQRT(25);
```

Result:

```text
5
```

---

# 6. String Functions

String functions text/data ke saath kaam karti hain.

## UPPER()

Text ko uppercase mein convert karta hai.

```sql
SELECT UPPER('ali');
```

Result:

```text
ALI
```

### Table Example

```sql
SELECT UPPER(stName)
FROM student;
```

Agar:

```text
stName = 'Ali'
```

to result:

```text
ALI
```

---

## LOWER()

Text ko lowercase mein convert karta hai.

```sql
SELECT LOWER('AHMED');
```

Result:

```text
ahmed
```

Example:

```sql
SELECT LOWER(stFName)
FROM student;
```

---

## LEN()

String ki length return karta hai.

```sql
SELECT LEN('Pakistan');
```

Result:

```text
8
```

Example:

```sql
SELECT LEN(stAdres)
FROM student;
```

---

## SUBSTRING()

String ka specific portion nikalne ke liye use hota hai.

Example:

```sql
SELECT SUBSTRING('Pakistan', 1, 4);
```

Result:

```text
Paki
```

> **Note:** Exact syntax/version database system ke mutabiq thora different ho sakta hai.

---

# 7. Date Functions

Date aur time ke saath kaam karne ke liye date functions use hoti hain.

Important examples:

```text
GETDATE()
DATEDIFF()
DATEPART()
```

## GETDATE()

Current date/time return karta hai.

```sql
SELECT GETDATE();
```

---

## DATEDIFF()

Do dates ke darmiyan difference nikalne ke liye use hota hai.

Example:

```sql
SELECT DATEDIFF(YEAR, '2020-01-01', '2026-01-01');
```

Result approximately:

```text
6
```

---

## DATEPART()

Date ka specific part nikal sakta hai.

Example:

```sql
SELECT DATEPART(YEAR, '2026-07-30');
```

Result:

```text
2026
```

---

# 8. Conversion Functions

Conversion functions ek data type ko doosre data type mein convert karti hain.

Important functions:

```text
CAST()
CONVERT()
```

## CAST()

```sql
SELECT CAST(100 AS VARCHAR);
```

Yahan number ko character/string type mein convert kiya ja raha hai.

---

## CONVERT()

```sql
SELECT CONVERT(CHAR, 100);
```

Ye bhi value ko doosre data type mein convert karta hai.

---

# 9. Nested Functions ⭐

## 🔹 Nested Function kya hota hai?

Jab ek function ke andar doosra function use kiya jaye, usay **Nested Function** kehte hain.

Example:

```sql
SELECT LEN(CONVERT(CHAR, stAdres))
FROM student;
```

Yahan:

```text
CONVERT()
```

pehle execute hoga.

Us ke baad:

```text
LEN()
```

converted value ki length calculate karega.

### Execution ko simple way mein samjho:

```text
stAdres
   ↓
CONVERT()
   ↓
Character value
   ↓
LEN()
   ↓
Length
```

### ⭐ Important Exam Point

**Nested function mein generally inner function pehle evaluate hota hai.**

---

# 10. Lecture ka Example — Multiple Functions

```sql
SELECT
    UPPER(stName),
    LOWER(stFName),
    stAdres,
    LEN(CONVERT(CHAR, stAdres))
FROM student;
```

Is query mein:

### `UPPER(stName)`

Student ka naam uppercase mein show hoga.

### `LOWER(stFName)`

Father name lowercase mein show hoga.

### `stAdres`

Address normally show hoga.

### `LEN(CONVERT(CHAR, stAdres))`

Address ko character mein convert karke uski length calculate ki jayegi.

---

# 11. Aggregate Functions ⭐⭐⭐

## 🔹 Aggregate Function kya hota hai?

Aggregate functions **multiple rows par operation** karti hain aur ek aggregate result return karti hain.

Important aggregate functions:

```text
AVG()
COUNT()
COUNT(*)
MIN()
MAX()
SUM()
```

---

# 12. AVG() — Average

Average calculate karta hai.

### Example

Student CGPA:

| Student | CGPA |
|---|---:|
| Ali | 3.00 |
| Sara | 3.50 |
| Ahmed | 4.00 |

Query:

```sql
SELECT AVG(cgpa)
FROM student;
```

Calculation:

```text
(3.00 + 3.50 + 4.00) / 3 = 3.50
```

Result:

```text
3.50
```

### Lecture Example

```sql
SELECT AVG(cgpa) AS 'Average CGPA'
FROM student;
```

---

# 13. COUNT() — Rows Count Karna

`COUNT()` rows ki number calculate karta hai.

## COUNT(*)

Table ki all rows count karta hai.

```sql
SELECT COUNT(*)
FROM student;
```

Agar table mein 100 students hain:

```text
100
```

### Example

```sql
SELECT COUNT(*) AS 'Total Students'
FROM student;
```

---

# 14. MIN() — Minimum Value

Sab se choti value nikalta hai.

```sql
SELECT MIN(cgpa)
FROM student;
```

Agar CGPAs hain:

```text
2.5, 3.0, 3.4, 3.9
```

to result:

```text
2.5
```

---

# 15. MAX() — Maximum Value

Sab se bari value nikalta hai.

```sql
SELECT MAX(cgpa)
FROM student;
```

Result:

```text
3.9
```

---

# 16. SUM() — Total

Values ka total nikalta hai.

Example:

```sql
SELECT SUM(salary)
FROM employees;
```

Agar salaries:

```text
30000
40000
50000
```

to total:

```text
120000
```

---

# 17. Aggregate Functions ka Quick Table

| Function | Meaning | Example |
|---|---|---|
| `AVG()` | Average | `AVG(cgpa)` |
| `COUNT()` | Count | `COUNT(id)` |
| `COUNT(*)` | All rows count | `COUNT(*)` |
| `MIN()` | Smallest value | `MIN(salary)` |
| `MAX()` | Largest value | `MAX(salary)` |
| `SUM()` | Total | `SUM(salary)` |

---

# 18. GROUP BY Clause ⭐⭐⭐

## 🔹 GROUP BY kya karta hai?

`GROUP BY` same values ko **groups** mein divide karta hai.

Ye especially aggregate functions ke saath use hota hai.

### Simple Example

Employees:

| Employee | Department | Salary |
|---|---|---:|
| Ali | IT | 50000 |
| Sara | IT | 60000 |
| Ahmed | HR | 40000 |
| Hina | HR | 45000 |

Agar humein **department-wise total salary** chahiye:

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

### Result

| Department | Total Salary |
|---|---:|
| IT | 110000 |
| HR | 85000 |

### Samajhne ka easy tareeqa

`GROUP BY department`

ka matlab:

> Pehle same department walon ko ek group banao.

Phir:

```text
SUM(salary)
```

har group ki salary ka total nikalta hai.

---

# 19. GROUP BY ka Important Rule ⭐

Agar `SELECT` mein koi normal column aggregate function ke bahar likha hai, to us column ko usually `GROUP BY` mein bhi include karna hota hai.

### Correct

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

### Why?

Kyunkay:

```text
department → normal column
SUM(salary) → aggregate function
```

Is liye:

```sql
GROUP BY department
```

---

# 20. GROUP BY — Lecture Example

```sql
SELECT department, SUM(sales) AS 'Total Sales'
FROM order_details
GROUP BY department;
```

Ye har department ki total sales return karega.

---

# 21. COUNT() with GROUP BY

Department-wise employees count karna:

```sql
SELECT department, COUNT(*) AS 'Number of Employees'
FROM employees
GROUP BY department;
```

### Example Result

| Department | Number of Employees |
|---|---:|
| IT | 15 |
| HR | 8 |
| Finance | 12 |

---

# 22. WHERE + GROUP BY

Agar pehle kuch rows filter karni hon aur phir groups banana hon, to `WHERE` use karte hain.

### Example

Sirf un employees ko consider karo jin ki salary 25,000 se zyada hai:

```sql
SELECT department, COUNT(*) AS 'Number of Employees'
FROM employees
WHERE salary > 25000
GROUP BY department;
```

### Is query ka process

```text
1. WHERE salary > 25000
        ↓
2. Remaining rows
        ↓
3. GROUP BY department
        ↓
4. COUNT(*)
```

---

# 23. HAVING Clause ⭐⭐⭐

## 🔹 HAVING kya hai?

`HAVING` ka use **GROUP BY ke baad groups ko filter** karne ke liye hota hai.

Ye specially aggregate results par condition lagane ke liye useful hai.

### Syntax

```sql
SELECT column1, aggregate_function(column)
FROM table_name
WHERE condition
GROUP BY column1
HAVING aggregate_function(column) condition;
```

---

# 24. HAVING ka Real Example — SUM()

Sirf woh departments show karne hain jinki total sales **1000 se zyada** hain:

```sql
SELECT department, SUM(sales) AS 'Total Sales'
FROM order_details
GROUP BY department
HAVING SUM(sales) > 1000;
```

### Samajho

Pehle:

```text
Department-wise sales calculate hongi.
```

Phir:

```text
Sirf woh departments show honge
jinki total sales > 1000 hain.
```

---

# 25. HAVING with COUNT()

Lecture example:

```sql
SELECT department, COUNT(*) AS 'Number of Employees'
FROM employees
WHERE salary > 25000
GROUP BY department
HAVING COUNT(*) > 10;
```

Iska simple meaning:

> Pehle salary 25,000 se zyada walay employees lo, phir department-wise groups banao, phir sirf woh departments show karo jahan employees ki count 10 se zyada hai.

---

# 26. WHERE vs HAVING ⭐⭐⭐

Ye difference exam mein bohat important hai.

| WHERE | HAVING |
|---|---|
| Individual rows ko filter karta hai | Groups ko filter karta hai |
| `GROUP BY` se pehle use hota hai | `GROUP BY` ke baad use hota hai |
| Row-level condition | Group-level condition |
| Aggregate result ke liye normally nahi | Aggregate functions ke saath use hota hai |

### WHERE Example

```sql
SELECT *
FROM employees
WHERE salary > 25000;
```

Meaning:

> Sirf woh rows jahan salary 25,000 se zyada hai.

### HAVING Example

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

Meaning:

> Sirf woh departments jinka total salary bill 100,000 se zyada hai.

---

# 27. WHERE + GROUP BY + HAVING

Ye combination bohat important hai.

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
WHERE salary > 25000
GROUP BY department
HAVING COUNT(*) > 10;
```

### Step-by-step:

```text
WHERE
↓
Rows filter karo

GROUP BY
↓
Rows ko groups mein divide karo

COUNT()
↓
Har group ki count nikaalo

HAVING
↓
Groups filter karo
```

---

# 28. SQL Query ka Important Logical Flow

Exam ke liye is flow ko yaad rakho:

```text
FROM
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY
```

Simple memory trick:

> **FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY**

Lekin query likhte waqt syntax order yeh hota hai:

```sql
SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...;
```

---

# 29. Accessing Multiple Tables

Ab tak hum mostly single table se data le rahe thay.

Real database mein data multiple tables mein hota hai.

Example:

```text
Student
Course
Program
Class
```

In tables se combined data retrieve karna ho sakta hai.

Lecture mein multiple-table access ke methods mention kiye gaye hain:

1. Cartesian Product
2. Inner Join
3. Outer Join
4. Full Outer Join
5. Semi Join
6. Natural Join

> **Lecture 30 mein mainly Cartesian Product explain kiya gaya hai. Baqi joins coming lectures mein detail se discuss hote hain.**

---

# 30. Referential Integrity

Multiple tables ko connect karte waqt **referential integrity** important hoti hai.

Simple idea:

> Ek table ka foreign key related table ke valid primary key ko refer kare.

Example:

### Program

| program_id | program_name |
|---:|---|
| 1 | BSCS |
| 2 | BSSE |

### Student

| student_id | name | program_id |
|---:|---|---:|
| 101 | Ali | 1 |
| 102 | Sara | 2 |

Yahan:

```text
Student.program_id
        ↓
Program.program_id
```

Student table ka `program_id` related Program ko refer karta hai.

---

# 31. Cartesian Product ⭐⭐⭐

## 🔹 Cartesian Product kya hai?

Cartesian Product mein first table ki **har row** second table ki **har row** ke saath combine hoti hai.

### Formula

Agar:

```text
Table A = m rows
Table B = n rows
```

to:

```text
Cartesian Product = m × n rows
```

---

# 32. Cartesian Product — Simple Example

### Program Table

| program |
|---|
| BSCS |
| BSSE |

Total:

```text
2 rows
```

### Course Table

| course |
|---|
| DBMS |
| OOP |
| DSA |

Total:

```text
3 rows
```

Cartesian Product:

```text
2 × 3 = 6 rows
```

---

# 33. Cartesian Product Query

```sql
SELECT *
FROM program, course;
```

Is query mein `program` ki har row ko `course` ki har row ke saath combine kiya jayega.

### Conceptual Result

| Program | Course |
|---|---|
| BSCS | DBMS |
| BSCS | OOP |
| BSCS | DSA |
| BSSE | DBMS |
| BSSE | OOP |
| BSSE | DSA |

Total:

```text
6 rows
```

---

# 34. Cartesian Product mein Specific Columns

Agar do tables mein same column name ho, to table name se column ko qualify kar sakte hain.

Example:

```sql
SELECT program.program_id, course.course_id
FROM program, course;
```

Yahan:

```text
program.program_id
```

ka matlab:

> `program` table ka `program_id`

Aur:

```text
course.course_id
```

ka matlab:

> `course` table ka `course_id`

---

# 35. Three Tables ka Cartesian Product

Cartesian Product multiple tables par bhi apply ho sakta hai.

Example:

```sql
SELECT *
FROM student, class, program;
```

Agar:

```text
Student = 5 rows
Class   = 3 rows
Program = 2 rows
```

to result:

```text
5 × 3 × 2 = 30 rows
```

---

# 36. Cartesian Product ko Real-Life Example se Samjhein

Suppose:

### T-Shirts

```text
Red
Blue
```

### Sizes

```text
Small
Medium
Large
```

Har color ko har size ke saath combine karein:

```text
Red   + Small
Red   + Medium
Red   + Large
Blue  + Small
Blue  + Medium
Blue  + Large
```

Total:

```text
2 × 3 = 6 combinations
```

Yehi basic idea Cartesian Product ka hai.

---

# 37. Cartesian Product ka Important Point

Cartesian Product mein generally **matching condition nahi hoti**.

Is liye agar tables bari hon to result mein bohat zyada rows aa sakti hain.

Example:

```text
100 students × 50 courses
= 5,000 rows
```

---

# 🧠 Important Concepts at a Glance

## ORDER BY

```sql
ORDER BY column ASC;
```

➡️ Sorting

---

## UPPER()

```sql
UPPER(name)
```

➡️ Uppercase

---

## LOWER()

```sql
LOWER(name)
```

➡️ Lowercase

---

## LEN()

```sql
LEN(address)
```

➡️ Length

---

## AVG()

```sql
AVG(cgpa)
```

➡️ Average

---

## COUNT()

```sql
COUNT(*)
```

➡️ Number of rows

---

## MIN()

```sql
MIN(salary)
```

➡️ Minimum

---

## MAX()

```sql
MAX(salary)
```

➡️ Maximum

---

## SUM()

```sql
SUM(salary)
```

➡️ Total

---

## GROUP BY

```sql
GROUP BY department
```

➡️ Groups banata hai

---

## HAVING

```sql
HAVING SUM(sales) > 1000
```

➡️ Groups ko filter karta hai

---

## WHERE

```sql
WHERE salary > 25000
```

➡️ Rows ko filter karta hai

---

## Cartesian Product

```sql
FROM table1, table2
```

➡️ Every row of table1 × every row of table2

---

# ⭐ Most Important Exam Differences

## 1. WHERE vs HAVING

```text
WHERE  → Rows
HAVING → Groups
```

---

## 2. ORDER BY vs GROUP BY

```text
ORDER BY → Sorting
GROUP BY  → Grouping
```

---

## 3. COUNT vs SUM

```text
COUNT → Kitni rows?
SUM   → Total kitna?
```

---

## 4. AVG vs SUM

```text
AVG → Average
SUM → Total
```

---

## 5. MIN vs MAX

```text
MIN → Sab se choti value
MAX → Sab se bari value
```

---

# 🧪 Practice Queries

## Practice 1 — Highest CGPA

```sql
SELECT MAX(cgpa)
FROM student;
```

---

## Practice 2 — Average CGPA

```sql
SELECT AVG(cgpa)
FROM student;
```

---

## Practice 3 — Total Students

```sql
SELECT COUNT(*)
FROM student;
```

---

## Practice 4 — Department-wise Employees

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

---

## Practice 5 — Department-wise Total Salary

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department;
```

---

## Practice 6 — Salary Filter

```sql
SELECT *
FROM employees
WHERE salary > 25000;
```

---

## Practice 7 — Departments with High Total Salary

```sql
SELECT department, SUM(salary)
FROM employees
GROUP BY department
HAVING SUM(salary) > 100000;
```

---

## Practice 8 — Sort Students

```sql
SELECT name, cgpa
FROM student
ORDER BY cgpa DESC;
```

---

## Practice 9 — Cartesian Product

```sql
SELECT *
FROM student, course;
```

---

## Practice 10 — WHERE + GROUP BY + HAVING

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
WHERE salary > 25000
GROUP BY department
HAVING COUNT(*) > 10;
```

---

# 📝 Lecture 30 — One-Page Revision

```text
ORDER BY
    ↓
Result ko sort karta hai
ASC = Ascending
DESC = Descending

FUNCTIONS
    ↓
Input/process karke result return karti hain

MATHEMATICAL
    ↓
ABS, ROUND, SIN, SQRT

STRING
    ↓
LOWER, UPPER, SUBSTRING, LEN

DATE
    ↓
DATEDIFF, DATEPART, GETDATE

SYSTEM
    ↓
USER, DATALENGTH, HOST_NAME

CONVERSION
    ↓
CAST, CONVERT

AGGREGATE FUNCTIONS
    ↓
AVG, COUNT, MIN, MAX, SUM

GROUP BY
    ↓
Same values ke groups banata hai

HAVING
    ↓
Groups ko filter karta hai

WHERE
    ↓
Rows ko filter karta hai

MULTIPLE TABLES
    ↓
Cartesian Product
Inner Join
Outer Join
Full Outer Join
Semi Join
Natural Join

CARTESIAN PRODUCT
    ↓
Every row × Every row

m rows × n rows = m × n rows
```

---

# 🚨 Last-Minute Exam Cheat Sheet

### Yaad Karne Wali Definitions

**ORDER BY:**  
Result set ko ascending ya descending order mein arrange karta hai.

**Function:**  
Ek special SQL operation jo value/result return karta hai.

**Aggregate Function:**  
Multiple rows par operation karke aggregate result return karta hai.

**GROUP BY:**  
Rows ko one or more columns ki values ke according groups mein divide karta hai.

**HAVING:**  
Grouped data ko aggregate condition ki basis par filter karta hai.

**Cartesian Product:**  
Do tables ki har row ko doosri table ki har row ke saath combine karta hai.

---

# 🔥 Golden Rules

```text
ORDER BY = Sorting

WHERE = Rows ko filter karo

GROUP BY = Groups banao

HAVING = Groups ko filter karo

AVG = Average

COUNT = Count

MIN = Minimum

MAX = Maximum

SUM = Total

Cartesian Product = m × n
```

### SQL Query Structure

```sql
SELECT ...
FROM ...
WHERE ...
GROUP BY ...
HAVING ...
ORDER BY ...;
```

### Sabse Important Difference

```text
WHERE  → individual rows
HAVING → grouped rows
```

---

# ✅ Final Summary

Lecture 30 mein SQL ke **sorting, functions, aggregate functions aur grouping** concepts cover kiye gaye.

Sabse important topics:

1. `ORDER BY` → sorting
2. `UPPER()`, `LOWER()`, `LEN()` → string functions
3. `CAST()`, `CONVERT()` → conversion
4. `AVG()`, `COUNT()`, `MIN()`, `MAX()`, `SUM()` → aggregate functions
5. `GROUP BY` → groups
6. `HAVING` → groups ko filter
7. `WHERE` → rows ko filter
8. Cartesian Product → every row × every row

> ⭐ **Exam tip:** `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY` ka difference aur `AVG/COUNT/MIN/MAX/SUM` zaroor prepare karein. Cartesian Product ka **m × n formula** bhi yaad rakhein.
