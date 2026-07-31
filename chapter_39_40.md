# Lecture 39 & 40 — Database Views

> **Subject:** Database Management Systems (DBMS)  
> **Topic:** Views, Types of Views, Security, Data Independence, View Updates  
> **Purpose:** Simple + detailed revision notes with real-world examples

---

## 1. View Kya Hoti Hai?

**View ek virtual table hoti hai jo kisi SQL query ke result se banti hai.**

Simple words mein:

- Base table mein actual data hota hai.
- View us data ka selected/filtered form dikhati hai.
- View ko SQL statements mein table ki tarah use kiya ja sakta hai.
- View ka main purpose **data ko focus, simplify aur secure** karna hai.

### Real-Life Example

University ki `STUDENT` table mein bohat zyada information ho sakti hai:

```text
Student
--------------------------------------------------
ID | Name | FatherName | Age | Program | GPA | Fee
```

Teacher ko sirf ye information chahiye:

```text
ID | Name | Program
```

Hum ek view bana sakte hain:

```sql
CREATE VIEW StudentBasic AS
SELECT ID, Name, Program
FROM Student;
```

Ab:

```sql
SELECT * FROM StudentBasic;
```

Result:

```text
ID | Name | Program
--------------------
1  | Ali  | BSCS
2  | Sara | BSSE
3  | Ahmed| BBA
```

Teacher ko unnecessary fields nahi dikh rahe.

---

# 2. View ko "Virtual Table" Kyun Kehte Hain?

View ko virtual table is liye kehte hain kyun ke ye base table ki tarah data ka logical representation provide karti hai, lekin ordinary/dynamic views ka result alag se permanently store nahi hota.

Example:

```text
EMPLOYEE Table
      |
      | SELECT * FROM EMPLOYEE
      v
   EMPLOYEE_VIEW
      |
      v
    User
```

Agar user:

```sql
SELECT * FROM EMPLOYEE_VIEW;
```

karta hai to view apni definition ke mutabiq data show karti hai.

### Important Exam Definition

> **A view is a virtual table based on the result of a SQL query.**

---

# 3. Views Kyun Use Hoti Hain?

Views ke 3 major purposes:

## A. Focus

User ko sirf required information dikhana.

Example:

HR department ko employees ke:

- Employee ID
- Name
- Department

chahiye.

Salary aur personal information hide ki ja sakti hai.

---

## B. Security

Views users ko restricted data provide kar sakti hain.

Example:

Base table:

```text
STUDENT
---------------------------------------------------
ID | Name | Age | Program | GPA | Password
```

Student ke liye:

```text
ID | Name | Age | Program
```

show karna hai.

```sql
CREATE VIEW StudentPublic AS
SELECT ID, Name, Age, Program
FROM STUDENT;
```

Ab students ko view ka access diya ja sakta hai, base table ka direct access nahi.

### Security Idea

```text
Sensitive Base Table
        |
        v
      VIEW
        |
        v
Authorized User
```

### Important Point

View security ka **logical layer** provide karti hai, lekin actual protection ke liye database permissions/privileges bhi correctly configure karne hote hain.

---

## C. Simplification

Agar ek query bohat complex ho aur baar baar use karni ho, to usay view mein define kar dete hain.

Instead of repeatedly writing:

```sql
SELECT E.Name, D.DepartmentName
FROM Employee E
JOIN Department D
ON E.DepartmentID = D.DepartmentID
WHERE E.Salary > 50000;
```

Hum view bana sakte hain:

```sql
CREATE VIEW HighSalaryEmployees AS
SELECT E.Name, D.DepartmentName
FROM Employee E
JOIN Department D
ON E.DepartmentID = D.DepartmentID
WHERE E.Salary > 50000;
```

Ab simply:

```sql
SELECT * FROM HighSalaryEmployees;
```

---

# 4. View ki Common Features

Views ko customize kiya ja sakta hai, for example:

- View ka naam
- Show hone wale fields
- Column names/titles
- Field order
- Rows ka selection
- Filtering
- Sorting
- Grouping
- Totals/subtotals

SQL level par ye kaam query ki clauses se hota hai, jaise:

```sql
SELECT
FROM
WHERE
GROUP BY
ORDER BY
```

---

# 5. View Banane Ka Basic Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

### Example

```sql
CREATE VIEW MCSStudents AS
SELECT stName, stFname, prName
FROM Student
WHERE prName = 'MCS';
```

View use karna:

```sql
SELECT * FROM MCSStudents;
```

---

# 6. Vertical Subset of a Table

**Vertical subset ka matlab hai columns select karna.**

Suppose original table:

```text
STUDENT
------------------------------------------------
ID | Name | Age | Program | GPA | City
```

Agar view:

```text
ID | Name | Program
```

show karti hai, to humne **columns** select kiye.

```sql
CREATE VIEW StudentInfo AS
SELECT ID, Name, Program
FROM Student;
```

### Yaad Rakhein

> **Vertical = Columns**

---

# 7. Horizontal Subset of a Table

**Horizontal subset ka matlab hai rows select karna.**

Suppose table:

```text
ID | Name  | Program
---------------------
1  | Ali   | BSCS
2  | Sara  | BBA
3  | Ahmed | BSCS
```

Sirf BSCS students chahiye:

```sql
CREATE VIEW BSCSStudents AS
SELECT *
FROM Student
WHERE Program = 'BSCS';
```

Result:

```text
1 | Ali   | BSCS
3 | Ahmed | BSCS
```

Humne specific **rows** select ki hain.

### Yaad Rakhein

> **Horizontal = Rows**

---

# 8. Vertical vs Horizontal Subset

| Feature | Vertical Subset | Horizontal Subset |
|---|---|---|
| Select kya hota hai? | Columns | Rows |
| Main idea | Required fields | Required records |
| Example | Name, Age, Program | Only BSCS students |
| SQL | SELECT specific columns | WHERE condition |

### Easy Trick

```text
VERTICAL   -> Columns
HORIZONTAL -> Rows
```

---

# 9. View Using Two Tables

Views multiple tables se bhi ban sakti hain.

Suppose:

### EMPLOYEE

```text
EmpID | Name | StoreID
-----------------------
1     | Ali  | 10
2     | Sara | 20
```

### STORE

```text
StoreID | StoreName
--------------------
10      | Karachi
20      | Lahore
```

Humein employee name aur store name saath chahiye:

```sql
CREATE VIEW EmployeeStore AS
SELECT E.Name, S.StoreName
FROM EMPLOYEE E
JOIN STORE S
ON E.StoreID = S.StoreID;
```

View result:

```text
Name | StoreName
-----------------
Ali  | Karachi
Sara | Lahore
```

### Concept

```text
EMPLOYEE + STORE
      |
     JOIN
      |
      v
 EmployeeStore View
```

Is type ki view generally **complex view** ho sakti hai.

---

# 10. View of a View

Ek view ko use karke doosri view bana sakte hain.

Isay **Nesting of Views** kehte hain.

### Example 1

```sql
CREATE VIEW CLASSLOC2 AS
SELECT COURSE#, ROOM
FROM CLASSLOC;
```

Ab `CLASSLOC2` ek view hai.

### Example 2

```sql
CREATE VIEW CLASSLOC3 AS
SELECT COURSE#
FROM CLASSLOC2;
```

Ab:

```text
CLASSLOC Table
      |
      v
 CLASSLOC2 View
      |
      v
 CLASSLOC3 View
```

### Important Term

> **View based on another view = Nested/Nesting View**

---

# 11. View Using a Function

View mein aggregate functions bhi use ki ja sakti hain.

Common functions:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

### Example

Suppose `ENROLL` table:

```text
COURSE# | StudentID
---------------------
CS101   | 1
CS101   | 2
CS101   | 3
CS201   | 4
CS201   | 5
```

Har course mein kitne students enrolled hain?

```sql
CREATE VIEW CLASSCOUNT (COURSE#, TOTCOUNT)
AS
SELECT COURSE#, COUNT(*)
FROM ENROLL
GROUP BY COURSE#;
```

Result:

```text
COURSE# | TOTCOUNT
-------------------
CS101   | 3
CS201   | 2
```

### Meaning

`COUNT(*)` = rows ko count karega.

`GROUP BY COURSE#` = har course ka separate count.

---

# 12. Types of Views

Lecture mein important types:

1. Materialized View
2. Simple View
3. Complex View
4. Dynamic View

---

# 13. Materialized View

**Materialized view query ka result physically store karti hai.**

Isay ek stored snapshot/result samajh sakte hain.

Example idea:

```text
Base Tables
    |
    v
  Query
    |
    v
Materialized View
    |
    v
Stored Result
```

Agar base data change hota hai, materialized view ko **refresh/update** karna pad sakta hai.

### Real Example

Large company ke sales database mein:

```text
Millions of sales records
        |
      Query
        |
        v
Monthly Sales Summary
```

Agar monthly summary materialized view mein store hai, to reporting fast ho sakti hai.

### Important

> **Materialized View = Result physically stored**

---

# 14. Simple View

Simple view generally ek base table par based hoti hai aur query simple hoti hai.

Example:

```sql
CREATE VIEW StudentNames AS
SELECT ID, Name
FROM Student;
```

### Simple View ki common idea

```text
One Table
   |
   v
Simple View
```

### Exam Point

Simple views, suitable conditions ke under, updates ko support kar sakti hain.

---

# 15. Complex View

Complex view mein multiple database objects/operations ho sakte hain.

For example:

- Multiple tables
- JOIN
- Functions
- Aggregate functions
- Other views
- Computed columns

Example:

```sql
CREATE VIEW StudentCourseSummary AS
SELECT S.Name, C.CourseName, COUNT(E.StudentID) AS TotalStudents
FROM Student S
JOIN Enrollment E
ON S.ID = E.StudentID
JOIN Course C
ON E.CourseID = C.CourseID
GROUP BY S.Name, C.CourseName;
```

Ye simple view se zyada complex hai.

### Easy Formula

```text
Multiple Tables / JOIN / Functions / Views
                    |
                    v
              Complex View
```

---

# 16. Dynamic View

Dynamic view mein result ko ordinary dynamic view ke context mein **access ke time query ke through generate** kiya jata hai.

Example:

```sql
CREATE VIEW st_view1 AS
SELECT stName, stFname, prName
FROM student
WHERE prName = 'MCS';
```

Ab:

```sql
SELECT * FROM st_view1;
```

View current underlying table ke data ko query ke mutabiq show karegi.

Agar underlying student records change hon aur view dobara access ki jaye, to result current data ke mutabiq change ho sakta hai.

### Important

> **Dynamic View = Data/result is generated dynamically from the underlying query when accessed.**

---

# 17. Materialized vs Dynamic View

| Materialized View | Dynamic View |
|---|---|
| Result physically stored | Result generally query se dynamically generated |
| Refresh required ho sakta hai | Access ke waqt current result generate hota hai |
| Reporting/performance ke liye useful | Current/fresh logical view ke liye useful |
| Storage consume karti hai | Ordinary dynamic view ka separate result storage nahi hota |

### Easy Trick

```text
Materialized = Stored Result
Dynamic      = Generated Result
```

---

# 18. Dynamic View Example

```sql
CREATE VIEW st_view1 AS
SELECT stName, stFname, prName
FROM student
WHERE prName = 'MCS';
```

Use:

```sql
SELECT * FROM st_view1;
```

Ye sirf MCS students ko dikhayegi.

---

# 19. WITH CHECK OPTION

**WITH CHECK OPTION bohat important concept hai.**

Ye ensure karta hai ke view ke through ki gayi `INSERT`/`UPDATE` operation view ki `WHERE` condition ko violate na kare.

### Example

```sql
CREATE VIEW st_view2 AS
SELECT stName, stFname, prName
FROM student
WHERE prName = 'BCS'
WITH CHECK OPTION;
```

View sirf:

```text
BCS Students
```

dikhati hai.

Ab:

```sql
UPDATE st_view2
SET prName = 'MCS'
WHERE stFname = 'Loving';
```

Ye normally reject hogi kyun ke `MCS` row view ki condition:

```sql
prName = 'BCS'
```

ko satisfy nahi karti.

### Simple Example

```text
View condition:
Program = 'BCS'

BCS -> BCS       ✅ Allowed
BCS -> MCS       ❌ Not Allowed
```

### Exam Definition

> **WITH CHECK OPTION prevents updates or inserts through the view from creating rows that do not satisfy the view condition.**

---

# 20. Without CHECK OPTION

Agar view:

```sql
CREATE VIEW BCSView AS
SELECT *
FROM Student
WHERE Program = 'BCS';
```

ho aur check option na ho, to kuch DBMS situations mein view ke through aisi modification possible ho sakti hai jis se row view ki condition ke bahar chali jaye.

`WITH CHECK OPTION` is risk ko restrict karta hai.

---

# 21. Computed Attributes in Views

View mein calculated/computed columns bana sakte hain.

Suppose:

```text
smrks = sessional marks
mterm = mid-term marks
```

Hum total/sessionals calculate karna chahte hain:

```sql
CREATE VIEW enr_view AS
SELECT * FROM enroll;
```

Then:

```sql
CREATE VIEW enr_view1 AS
SELECT stId,
       crcode,
       smrks,
       mterm,
       smrks + mterm AS sessional
FROM enr_view;
```

Yahan:

```text
sessional = smrks + mterm
```

### Example

```text
smrks = 20
mterm = 25

sessional = 45
```

`sessional` base table ka original stored field nahi, balki **computed attribute** hai.

---

# 22. View Updates

Question:

> Kya view ko update kar sakte hain?

### Answer

**Har view updateable nahi hoti.**

Simple views based on one table aur suitable columns ko update kiya ja sakta hai.

Example:

```sql
CREATE VIEW StudentBasic AS
SELECT ID, Name
FROM Student;
```

Possible update:

```sql
UPDATE StudentBasic
SET Name = 'Sara'
WHERE ID = 1;
```

Is operation ka effect underlying `Student` table par ho sakta hai, agar view updatable hai.

---

# 23. Complex Views ko Update Karna Mushkil Kyun Hai?

Suppose:

```text
Student + Course
      |
     JOIN
      |
      v
 StudentCourseView
```

Agar view mein:

- multiple tables
- joins
- aggregate functions
- `GROUP BY`
- computed columns

hon, to database ko determine karna mushkil ho sakta hai ke update kis base row/table ko affect kare.

Is liye complex views often **not directly updateable** ya restricted hoti hain.

---

# 24. Computed Attribute ko Update Karna

Suppose:

```text
sessional = smrks + mterm
```

Aur hum likhein:

```sql
UPDATE enr_view1
SET sessional = 50;
```

Problem ye hai:

```text
sessional = smrks + mterm
```

To database ko decide karna hoga:

```text
smrks change karun?
mterm change karun?
dono?
```

Isi wajah se computed attributes wali views generally directly updateable nahi hoti.

---

# 25. DELETE / DROP View

View delete karne ke liye:

```sql
DROP VIEW view_name;
```

Example:

```sql
DROP VIEW StudentBasic;
```

### Important

`DROP VIEW` se **sirf view remove hoti hai**.

Underlying/base table remove nahi hoti.

```text
Student Table
     |
     v
StudentBasic View

DROP VIEW StudentBasic;

Student Table -> Still Exists ✅
View          -> Deleted ❌
```

---

# 26. Views and Logical Data Independence

Ye theoretical aur important concept hai.

Database architecture mein conceptual schema aur external schema ka concept hota hai.

Views external users/applications ko required structure provide kar sakti hain.

Agar conceptual schema mein changes kar diye jayein, to suitable view ke through old interface maintain kiya ja sakta hai.

### Example

Old application expects:

```text
StudentID | Name | Program
```

Base table ka internal structure change ho jata hai.

Ek compatible view create karke old application ko same expected columns provide kiye ja sakte hain.

### Important Definition

> **Views support logical data independence by hiding suitable conceptual-schema changes from applications/users.**

---

# 27. Views for Security — Detailed Example

Suppose company ke paas:

```text
EMPLOYEE
------------------------------------------------
ID | Name | Salary | CNIC | Password | Dept
```

Normal employee ko sirf:

```text
ID | Name | Dept
```

show karna hai.

View:

```sql
CREATE VIEW EmployeePublic AS
SELECT ID, Name, Dept
FROM EMPLOYEE;
```

Employee:

```sql
SELECT * FROM EmployeePublic;
```

Result:

```text
ID | Name  | Dept
------------------
1  | Ali   | IT
2  | Sara  | HR
```

Sensitive data:

```text
Salary
CNIC
Password
```

view mein included nahi.

### Main Idea

> **Give access to the view, not necessarily to the complete base table.**

---

# 28. Complete Example — University Database

Suppose hamare paas:

### STUDENT

```text
stId | stName | stFname | prName | GPA
---------------------------------------
1    | Ali    | Ahmed   | BCS    | 3.2
2    | Sara   | Imran   | MCS    | 3.7
3    | Hamza  | Khalid  | BCS    | 3.5
4    | Ayesha | Tariq   | MCS    | 3.9
```

## View 1 — Only MCS Students

```sql
CREATE VIEW MCSStudents AS
SELECT stId, stName, prName
FROM STUDENT
WHERE prName = 'MCS';
```

Query:

```sql
SELECT * FROM MCSStudents;
```

Result:

```text
2 | Sara   | MCS
4 | Ayesha | MCS
```

This is a **horizontal subset** because rows are selected.

---

## View 2 — Only Basic Information

```sql
CREATE VIEW StudentBasic AS
SELECT stId, stName, prName
FROM STUDENT;
```

This is a **vertical subset** because selected columns are shown.

---

## View 3 — GPA Result View

```sql
CREATE VIEW StudentGPA AS
SELECT stId, stName, GPA
FROM STUDENT;
```

This focuses on only GPA-related information.

---

# 29. Most Important SQL Commands

## Create View

```sql
CREATE VIEW ViewName AS
SELECT ...
FROM ...
WHERE ...;
```

## Read View

```sql
SELECT * FROM ViewName;
```

## Update View

```sql
UPDATE ViewName
SET column = value
WHERE condition;
```

> Only if the view is updateable.

## Drop View

```sql
DROP VIEW ViewName;
```

## With Check Option

```sql
CREATE VIEW ViewName AS
SELECT ...
FROM ...
WHERE condition
WITH CHECK OPTION;
```

---

# 30. Important Differences for Exam

## View vs Table

| Table | View |
|---|---|
| Actual/base data store karti hai | Query-based logical/virtual representation |
| Independent data object | Base objects par depend karti hai |
| Direct records contain karti hai | Query result show karti hai |
| Physical data storage involved | Ordinary view ka result separately persist nahi hota |

---

## Simple View vs Complex View

| Simple View | Complex View |
|---|---|
| Usually one table | Multiple tables/views possible |
| Simple query | JOIN/functions/aggregate etc. possible |
| Often easier to update | Updates may be restricted |
| Less complicated | More complicated |

---

## Materialized View vs Dynamic View

| Materialized | Dynamic |
|---|---|
| Result stored | Result generated dynamically |
| Refresh may be needed | Query/access ke time result |
| Faster reads can be possible | Current underlying data reflect kar sakti hai |
| Storage required | Ordinary view ka separate result storage nahi |

---

## Vertical vs Horizontal

| Vertical | Horizontal |
|---|---|
| Columns | Rows |
| Field selection | Record selection |
| `SELECT ID, Name` | `WHERE Program='BCS'` |

---

# 31. Key Terms

### View
Virtual table based on a SQL query.

### Base Table
Original table jisme actual database records stored hote hain.

### Materialized View
Physically stored query result/snapshot.

### Simple View
Simple, usually single-table-based view.

### Complex View
Multiple tables, joins, functions, aggregates or other views wala view.

### Dynamic View
Access ke waqt query se result generate karne wali ordinary view.

### Nested View
A view created using another view.

### Computed Attribute
A column calculated from an expression, e.g.:

```sql
smrks + mterm
```

### WITH CHECK OPTION
View condition ko preserve karne ke liye restriction.

### DROP VIEW
View ko remove karne ka command.

---

# 32. Exam-Ready Definitions

## What is a View?

> A view is a virtual table created from the result of a SQL query. It is used to simplify data access, focus on required information and improve data security.

## What is a Materialized View?

> A materialized view stores the query result physically and may need to be refreshed when the underlying data changes.

## What is a Simple View?

> A simple view is generally created from a single base table using a simple query.

## What is a Complex View?

> A complex view may contain multiple tables, joins, functions, aggregate operations or other views.

## What is a Dynamic View?

> A dynamic view generates its result from its underlying query when it is accessed.

## What is WITH CHECK OPTION?

> It prevents modifications through a view from creating rows that do not satisfy the view's defining condition.

## What is Vertical Subset?

> A vertical subset selects specific columns from a table.

## What is Horizontal Subset?

> A horizontal subset selects specific rows from a table.

---

# 33. Expected Short Questions

### Q1. Why are views used?

**Answer:**

- Security
- Simplification
- Focus on specific data
- Logical data independence

### Q2. Can a view be treated like a table?

**Answer:**  
Yes. A view can generally be referenced in SQL queries like a table.

### Q3. Can a view contain data from multiple tables?

**Answer:**  
Yes, by using operations such as `JOIN`.

### Q4. Can a view use functions?

**Answer:**  
Yes. For example `COUNT()`, `SUM()`, `AVG()`, etc. can be used where the view/query rules allow them.

### Q5. Can one view be created from another view?

**Answer:**  
Yes. This is called nesting of views.

### Q6. Which command deletes a view?

```sql
DROP VIEW ViewName;
```

### Q7. What is a computed attribute?

**Answer:**  
A column whose value is calculated from other values, for example:

```sql
smrks + mterm AS sessional
```

---

# 34. Most Important Long Questions

Exam mein in topics ko detail mein prepare karo:

### 1. Explain views and their uses.

Include:

- Definition
- Virtual table
- Focus
- Security
- Simplification
- Example

### 2. Explain different types of views.

Include:

- Materialized
- Simple
- Complex
- Dynamic

### 3. Explain vertical and horizontal subsets.

Include:

- Vertical = columns
- Horizontal = rows
- SQL examples

### 4. Explain WITH CHECK OPTION.

Include:

- Definition
- `WHERE` condition
- Update example
- Why restriction is useful

### 5. Explain updates on views.

Include:

- Simple view may be updateable
- Complex views are often difficult/restricted
- Computed/aggregate results cause problems

### 6. Explain views and security.

Include:

- Hide sensitive columns
- Give user access to view
- Restrict direct base-table access

### 7. Explain views and logical data independence.

Include:

- External schema
- Hide suitable schema changes
- Application compatibility

---

# 35. One-Page Quick Revision

```text
VIEW
|
|-- Virtual Table
|
|-- Uses
|    |-- Security
|    |-- Focus
|    |-- Simplification
|    |-- Logical Data Independence
|
|-- Subsets
|    |-- Vertical = Columns
|    |-- Horizontal = Rows
|
|-- Types
|    |-- Materialized = Stored Result
|    |-- Simple = Usually One Table
|    |-- Complex = Multiple/Complex Operations
|    |-- Dynamic = Generated on Access
|
|-- Advanced
|    |-- View of View
|    |-- View using Function
|    |-- Computed Attributes
|    |-- WITH CHECK OPTION
|
|-- Operations
|    |-- CREATE VIEW
|    |-- SELECT FROM VIEW
|    |-- UPDATE (if updateable)
|    |-- DROP VIEW
```

---

# 36. Last-Minute Memory Tricks

### Trick 1

```text
Vertical   = Columns
Horizontal = Rows
```

### Trick 2

```text
Materialized = Material/Stored
Dynamic      = Dynamically Generated
```

### Trick 3

```text
WITH CHECK OPTION
        =
"View ki condition break mat karo"
```

### Trick 4

```text
Simple View
    ↓
One table / simple structure

Complex View
    ↓
Multiple tables / joins / functions / views
```

### Trick 5

```text
View Security
    ↓
User ko complete table nahi
sirf required data dikhao
```

---

# 37. Final Summary

Lecture 39 & 40 ka central idea **Views** hai.

A **view** database ki ek virtual representation hai jo SQL query ke result ko user ke liye table-like form mein show karti hai.

Views mainly:

- data ko **focus** karti hain,
- database ko **secure** banane mein help karti hain,
- complex queries ko **simple** banati hain,
- aur **logical data independence** support karti hain.

Important concepts:

```text
View                -> Virtual Table
Vertical Subset     -> Columns
Horizontal Subset   -> Rows
Materialized View   -> Stored Result
Simple View         -> Usually One Table
Complex View        -> Multiple/Complex Operations
Dynamic View        -> Generated Dynamically
Nested View         -> View of a View
Computed Attribute  -> Calculated Column
CHECK OPTION        -> Condition Must Remain True
DROP VIEW           -> Delete the View
```

## Most Important SQL Examples

```sql
-- 1. Simple View
CREATE VIEW StudentBasic AS
SELECT ID, Name, Program
FROM Student;

-- 2. Horizontal subset
CREATE VIEW BCSStudents AS
SELECT *
FROM Student
WHERE Program = 'BCS';

-- 3. View using multiple tables
CREATE VIEW EmployeeStore AS
SELECT E.Name, S.StoreName
FROM Employee E
JOIN Store S
ON E.StoreID = S.StoreID;

-- 4. View using function
CREATE VIEW ClassCount AS
SELECT COURSE#, COUNT(*) AS TotalCount
FROM Enroll
GROUP BY COURSE#;

-- 5. View with Check Option
CREATE VIEW BCSView AS
SELECT ID, Name, Program
FROM Student
WHERE Program = 'BCS'
WITH CHECK OPTION;

-- 6. Read a View
SELECT * FROM StudentBasic;

-- 7. Drop a View
DROP VIEW StudentBasic;
```

---

# ⭐ Exam Priority

Agar time bohat kam hai to is order mein revise karo:

1. **Definition of View**
2. **Uses: Security, Focus, Simplification**
3. **Vertical vs Horizontal**
4. **Simple vs Complex View**
5. **Materialized vs Dynamic View**
6. **WITH CHECK OPTION**
7. **Updates on Views**
8. **View using two tables**
9. **View of a View**
10. **View using Function**
11. **Computed Attributes**
12. **DROP VIEW**

> **Golden Line:**  
> `View = Virtual Table + Security + Simplification + Focus`

