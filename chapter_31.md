# 📚 DBMS – Lecture 31 Complete Notes

## Types of Joins, Subqueries & Access Control

**Course:** Database Management System (CS403) – Virtual University of Pakistan  
**Lecture:** 31  
**Main Topics:**
- Types of Joins
- Subquery / Nested Query
- Access Control
- GRANT and REVOKE
- DCL (Data Control Language)

---

# 📌 1. Lecture Overview

Lecture 31 mein hum SQL ke kuch bohat important concepts parhte hain:

1. **Inner Join**
2. **Outer Join**
   - Left Outer Join
   - Right Outer Join
   - Full Outer Join
3. **Semi Join**
4. **Self Join**
5. **Subquery / Nested Query**
6. **Access Control**
7. **GRANT command**
8. **REVOKE command**
9. **CASCADE and RESTRICT**
10. **WITH GRANT OPTION**

---

# 🔗 2. JOIN Kya Hota Hai?

### Simple Definition

**JOIN** SQL ka operation hai jo **do ya do se zyada tables ko kisi related/common attribute ki basis par combine karta hai.**

Real databases mein tables alag alag information store karti hain. Jab humein dono tables ki information ek saath chahiye hoti hai to JOIN use hota hai.

### Real-Life Example

Ek university mein:

### STUDENT Table

| stId | stName | prName |
|---|---|---|
| 1 | Ali | BCS |
| 2 | Sara | BSIT |
| 3 | Ahmed | BCS |

### PROGRAM Table

| prName | duration |
|---|---|
| BCS | 4 Years |
| BSIT | 4 Years |

Dono tables mein `prName` common hai.

Agar humein student ka naam aur uske program ki duration ek saath chahiye, to JOIN use karenge.

```sql
SELECT s.stName, s.prName, p.duration
FROM STUDENT s
INNER JOIN PROGRAM p
ON s.prName = p.prName;
```

### Result

| stName | prName | duration |
|---|---|---|
| Ali | BCS | 4 Years |
| Sara | BSIT | 4 Years |
| Ahmed | BCS | 4 Years |

---

# ⚠️ Cartesian Product vs JOIN

Previous lecture mein Cartesian Product discuss hua tha.

### Cartesian Product

Cartesian Product mein first table ki **har row** second table ki **har row** ke saath combine hoti hai.

Agar:

- Table A = 3 rows
- Table B = 4 rows

to Cartesian Product:

**3 × 4 = 12 rows**

Ye usually unwanted data bohat zyada produce karta hai.

### JOIN

JOIN sirf related/matching rows ko combine karta hai.

### Easy Difference

```text
Cartesian Product → Every row with every row
JOIN              → Related rows with matching condition
```

---

# ⭐ 3. INNER JOIN

## Definition

**Inner Join sirf un rows ko return karta hai jinka matching value dono tables mein milta hai.**

### Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

### Example

### COURSE

| courseId | courseName | prName |
|---|---|---|
| C01 | DBMS | BCS |
| C02 | OOP | BCS |
| C03 | AI | BSCS |
| C04 | Web | BSIT |

### PROGRAM

| prName | duration |
|---|---|
| BCS | 4 Years |
| BSIT | 4 Years |

Query:

```sql
SELECT *
FROM COURSE c
INNER JOIN PROGRAM p
ON c.prName = p.prName;
```

### Kya hoga?

- `BCS` ka match mil gaya ✅
- `BSIT` ka match mil gaya ✅
- `BSCS` ka match nahi mila ❌

Is liye `AI` wali row result mein nahi aayegi.

### Golden Rule

> **INNER JOIN = Matching rows only**

---

# 🔍 3.1 INNER JOIN ke 2 Common Methods

### Method 1 – Explicit INNER JOIN

```sql
SELECT *
FROM COURSE c
INNER JOIN PROGRAM p
ON c.prName = p.prName;
```

### Method 2 – WHERE ke saath

```sql
SELECT *
FROM COURSE c, PROGRAM p
WHERE c.prName = p.prName;
```

Dono matching condition ke basis par same type ka result de sakte hain.

---

# 📌 3.2 Common Attribute ka Name Same Hona Zaroori Nahi

Dono tables ke related columns ka naam same hona zaroori nahi.

Example:

```text
COURSE.programName
PROGRAM.prName
```

Query:

```sql
SELECT *
FROM COURSE c
INNER JOIN PROGRAM p
ON c.programName = p.prName;
```

Lekin dono attributes ka **domain/data type compatible** hona chahiye.

---

# 🌐 4. OUTER JOIN

## Definition

**Outer Join matching rows ke saath unmatched rows ko bhi result mein include karta hai.**

Jab kisi row ka match nahi milta to doosri table ke columns mein **NULL** aa jata hai.

Outer Join ke 3 main types hain:

1. LEFT OUTER JOIN
2. RIGHT OUTER JOIN
3. FULL OUTER JOIN

---

# ⭐ 5. LEFT OUTER JOIN

## Definition

**Left Join left table ki saari rows return karta hai, chahe right table mein match ho ya na ho.**

### Syntax

```sql
SELECT *
FROM COURSE c
LEFT OUTER JOIN PROGRAM p
ON c.prName = p.prName;
```

### Example

COURSE:

| courseId | courseName | prName |
|---|---|---|
| C01 | DBMS | BCS |
| C02 | OOP | BCS |
| C03 | AI | BSCS |

PROGRAM:

| prName | duration |
|---|---|
| BCS | 4 Years |
| BSIT | 4 Years |

`BSCS` ka PROGRAM table mein match nahi hai.

LEFT JOIN phir bhi `AI` ko result mein show karega:

| courseId | courseName | prName | duration |
|---|---|---|---|
| C01 | DBMS | BCS | 4 Years |
| C02 | OOP | BCS | 4 Years |
| C03 | AI | BSCS | NULL |

### Golden Rule

> **LEFT JOIN = Left table ki ALL rows**

---

# ⭐ 6. RIGHT OUTER JOIN

## Definition

**Right Join right table ki saari rows return karta hai, chahe left table mein match ho ya na ho.**

### Syntax

```sql
SELECT *
FROM COURSE c
RIGHT OUTER JOIN PROGRAM p
ON c.prName = p.prName;
```

Agar PROGRAM mein `BSIT` hai aur COURSE mein BSIT ki koi row nahi, to BSIT phir bhi result mein aayega aur COURSE side par NULL hoga.

### Golden Rule

> **RIGHT JOIN = Right table ki ALL rows**

---

# ⭐ 7. FULL OUTER JOIN

## Definition

**Full Outer Join dono tables ki saari rows return karta hai.**

Matching rows combine hoti hain.

Unmatched rows bhi show hoti hain aur doosri side ke columns mein NULL hota hai.

### Syntax

```sql
SELECT *
FROM COURSE c
FULL OUTER JOIN PROGRAM p
ON c.prName = p.prName;
```

### Golden Rule

> **FULL JOIN = Both tables ki ALL rows**

---

# 🧠 8. INNER vs LEFT vs RIGHT vs FULL JOIN

| JOIN | Kya return karta hai? |
|---|---|
| INNER JOIN | Sirf matching rows |
| LEFT JOIN | Left table ki all rows + matching right rows |
| RIGHT JOIN | Right table ki all rows + matching left rows |
| FULL OUTER JOIN | Dono tables ki all rows |

### One-Line Formula

```text
INNER → Match only
LEFT  → All Left
RIGHT → All Right
FULL  → All Both
```

---

# ⚠️ Important Note About Lecture Figure/Text

Kabhi kabhi lecture handout ke explanation mein LEFT aur RIGHT outer join ki wording confusing ya swapped nazar aa sakti hai. SQL ka standard concept yaad rakhein:

```text
LEFT JOIN  → LEFT table ki all rows
RIGHT JOIN → RIGHT table ki all rows
FULL JOIN  → BOTH tables ki all rows
```

Exam ke liye ye rule sabse important hai.

---

# 🎯 9. SEMI JOIN

## Definition

**Semi Join mein pehle inner join perform hota hai aur phir result ko sirf ek table ke attributes tak project kiya jata hai.**

Is se humein pata chalta hai ke kisi ek table ki kaun si rows doosri table mein match kar rahi hain.

### Real-Life Example

Humein sirf wo programs chahiye **jin ke andar courses available hain**.

```sql
SELECT DISTINCT p.prName, p.totsem, p.prCredits
FROM PROGRAM p
INNER JOIN COURSE c
ON p.prName = c.prName;
```

Yahan PROGRAM ki matching information rakhi gayi.

### Semi Join ka Main Idea

```text
INNER JOIN
     ↓
Matching rows
     ↓
Sirf one-table attributes
```

### Important

SQL mein normally direct `SEMI JOIN` keyword nahi hota. Is concept ko `INNER JOIN`, `SELECT`, aur zarurat par `DISTINCT` se implement kiya ja sakta hai.

---

# 🔁 10. SELF JOIN

## Definition

**Self Join mein ek table ko usi table ke saath join kiya jata hai.**

Ye tab useful hota hai jab table ke andar kisi row ka reference **usi table ki doosri row** se ho.

---

## Real-Life Example: Class Representative

### STUDENT Table

| stId | stName | cr |
|---|---|---|
| 1 | Ali | NULL |
| 2 | Sara | 3 |
| 3 | Ahmed | NULL |
| 4 | Hina | 3 |

Yahan `cr` mein class representative ka `stId` stored hai.

Sara ka `cr = 3` matlab uski class representative ka student ID 3 hai, yani Ahmed.

### Query

```sql
SELECT a.stId, a.stName, b.stId, b.stName
FROM STUDENT a, STUDENT b
WHERE a.cr = b.stId;
```

### Result ka idea

| Student | CR |
|---|---|
| Sara | Ahmed |
| Hina | Ahmed |

### Alias kyun use kiye?

Same table 2 baar use hui hai:

```text
STUDENT a → Student
STUDENT b → Class Representative
```

Is liye aliases zaroori hain taake columns clearly identify kiye ja saken.

### Golden Rule

> **SELF JOIN = Table joined with itself**

---

# 🧩 11. SUBQUERY / NESTED QUERY

## Definition

**Subquery ek query ke andar doosri query hoti hai.**

Isay **Nested Query** bhi kaha jata hai.

Usually subquery `WHERE` clause mein aati hai, lekin SQL mein subqueries doosri places par bhi use ho sakti hain.

---

# 🧠 11.1 Subquery ki Zarurat Kyun Hoti Hai?

Kabhi humein kisi condition ki value pehle calculate karni hoti hai, phir main query us result ko use karti hai.

### Example

Humein maximum CGPA wale student ka complete record chahiye.

Sirf:

```sql
SELECT MAX(cgpa)
FROM STUDENT;
```

maximum CGPA batayega, lekin student ki complete details nahi.

Is liye subquery use karenge.

```sql
SELECT *
FROM STUDENT
WHERE cgpa = (
    SELECT MAX(cgpa)
    FROM STUDENT
);
```

---

# 🔍 11.2 Main Query aur Subquery

Is example mein:

```sql
SELECT *
FROM STUDENT
WHERE cgpa = (
    SELECT MAX(cgpa)
    FROM STUDENT
);
```

### Subquery

```sql
SELECT MAX(cgpa)
FROM STUDENT
```

### Outer/Main Query

```sql
SELECT *
FROM STUDENT
WHERE cgpa = (...);
```

---

# ⏳ 11.3 Subquery Execution Order

Normally conceptually:

```text
1. Inner/Subquery execute
2. Result milta hai
3. Outer/Main query us result ko use karti hai
```

### Golden Rule

> **Inner → Outer**

Agar multiple levels ki nesting ho to deepest/innermost query pehle evaluate hoti hai.

---

# 🎯 12. Single-Value Subquery

Agar subquery **sirf ek value** return karti hai to hum normal comparison operators use kar sakte hain:

```text
=
>
<
>=
<=
<>
```

### Example

```sql
SELECT *
FROM STUDENT
WHERE cgpa > (
    SELECT MAX(cgpa)
    FROM STUDENT
    WHERE prName = 'BCS'
);
```

Yahan subquery ek single maximum value return karne ki expectation rakhti hai.

---

# 📚 13. Multiple-Value Subquery

Agar subquery multiple rows/values return kar sakti hai to `IN` ya `NOT IN` bohat useful hota hai.

### Example

```sql
SELECT *
FROM STUDENT
WHERE prName IN (
    SELECT prName
    FROM PROGRAM
);
```

Meaning:

> Wo students lao jinka program PROGRAM table ke generated set mein موجود hai.

### NOT IN

```sql
SELECT *
FROM STUDENT
WHERE prName NOT IN (
    SELECT prName
    FROM PROGRAM
);
```

Meaning:

> Wo students/program values lao jo subquery ke result mein nahi hain.

---

# 🧠 14. Single Value vs Multiple Values

| Subquery Result | Common Operators |
|---|---|
| Single value | `=`, `>`, `<`, `>=`, `<=`, `<>` |
| Multiple values | `IN`, `NOT IN` |

### Easy Memory Trick

```text
One value   → =, >, <, ...
Many values → IN / NOT IN
```

---

# 🔐 15. ACCESS CONTROL

## Definition

**Access Control database mein users ki permissions ko control karta hai.**

Example:

- User A sirf data read kar sakta hai.
- User B data insert/update kar sakta hai.
- User C data delete bhi kar sakta hai.

SQL mein access control ke important commands:

```text
GRANT
REVOKE
```

Ye **DCL (Data Control Language)** se related commands hain.

---

# ✅ 16. GRANT Command

## Definition

**GRANT kisi user ko privilege/permission dene ke liye use hota hai.**

### General Syntax

```sql
GRANT privileges
ON object
TO users
[WITH GRANT OPTION];
```

Yahan:

- `privileges` = permission
- `object` = table/view
- `users` = jinko permission deni hai

---

# 📌 16.1 SELECT Privilege

Table ka data read karne ki permission:

```sql
GRANT SELECT ON COURSE TO Mina;
```

Meaning:

> Mina COURSE table ko read kar sakti hai.

---

# 📌 16.2 INSERT Privilege

Rows insert karne ki permission:

```sql
GRANT INSERT ON COURSE TO Mina;
```

Specific column ke liye bhi privilege diya ja sakta hai:

```sql
GRANT INSERT(courseName) ON COURSE TO Mina;
```

---

# 📌 16.3 UPDATE Privilege

Existing values modify karne ki permission:

```sql
GRANT UPDATE ON COURSE TO Mina;
```

Specific column:

```sql
GRANT UPDATE(courseName) ON COURSE TO Mina;
```

---

# 📌 16.4 DELETE Privilege

Rows delete karne ki permission:

```sql
GRANT DELETE ON COURSE TO Mina;
```

---

# 📌 16.5 REFERENCES Privilege

Foreign key/reference define karne se related permission:

```sql
GRANT REFERENCES ON COURSE TO Mina;
```

Specific column par bhi diya ja sakta hai:

```sql
GRANT REFERENCES(courseId) ON COURSE TO Mina;
```

---

# ⭐ 17. WITH GRANT OPTION

Ye bohat important concept hai.

```sql
GRANT SELECT
ON COURSE
TO Alia
WITH GRANT OPTION;
```

Meaning:

> Alia ko COURSE par SELECT permission mili **aur Alia ye SELECT privilege kisi aur user ko bhi grant kar sakti hai.**

### Difference

Without `WITH GRANT OPTION`:

```text
Alia → SELECT kar sakti hai
```

With `WITH GRANT OPTION`:

```text
Alia → SELECT kar sakti hai
Alia → SELECT kisi aur ko bhi de sakti hai
```

### Example

```text
Javed
  │
  │ GRANT SELECT + GRANT OPTION
  ↓
Alia
  │
  │ GRANT SELECT
  ↓
Bobby
```

---

# 🔄 18. REVOKE Command

## Definition

**REVOKE kisi user se pehle di hui privilege/permission ko withdraw karne ke liye use hota hai.**

### Syntax

```sql
REVOKE privileges
ON object
FROM users
{RESTRICT | CASCADE};
```

### Example

```sql
REVOKE SELECT
ON COURSE
FROM Alia
CASCADE;
```

Meaning:

> Alia se COURSE par SELECT privilege revoke kar do; aur CASCADE ki wajah se dependent grants bhi revoke kiye ja sakte hain.

---

# 🌊 19. CASCADE

## Definition

**CASCADE ka matlab hai ke revoke ka effect dependent/granted privileges tak bhi propagate ho sakta hai.**

### Example

Javed ne Alia ko permission di:

```text
Javed → Alia → Bobby
```

Javed:

```sql
GRANT SELECT ON COURSE TO Alia WITH GRANT OPTION;
```

Alia:

```sql
GRANT SELECT ON COURSE TO Bobby WITH GRANT OPTION;
```

Ab Javed:

```sql
REVOKE SELECT
ON COURSE
FROM Alia
CASCADE;
```

Result ka concept:

```text
Alia → permission lost
Bobby → permission bhi lost ho sakti hai
```

Lekin agar Bobby ko wahi permission kisi aur independent source se mili hui thi, to Bobby ki permission retain ho sakti hai.

---

# 🚫 20. RESTRICT

**RESTRICT** ka idea ye hai ke agar revoke karne se doosri dependent privileges abandoned ho rahi hon, to revoke operation reject ho sakti hai.

### Easy Difference

```text
CASCADE  → Dependent privileges bhi remove kar sakti hai
RESTRICT → Dependent effect ho to revoke reject ho sakti hai
```

---

# 🔥 21. GRANT OPTION ko Sirf Revoke Karna

Kabhi hum user ki actual privilege remove nahi karna chahte, sirf uski **aage grant karne ki power** remove karna chahte hain.

### Query

```sql
REVOKE GRANT OPTION FOR
SELECT ON COURSE
FROM Alia
CASCADE;
```

### Result

```text
Alia ki SELECT permission      → ✅ rahegi
Alia ki grant karne ki power   → ❌ khatam
```

### Yaad rakho

```text
REVOKE SELECT
→ SELECT permission khatam

REVOKE GRANT OPTION FOR SELECT
→ SELECT permission rahegi
→ Lekin aage GRANT nahi kar sakti
```

---

# 👑 22. Table Creator ke Privileges

Lecture ke mutabiq base table ka creator automatically applicable privileges hold karta hai aur un privileges ko grant bhi kar sakta hai.

Similarly, schema owner hi `CREATE`, `ALTER`, aur `DROP` jaise data definition statements ko apne schema par execute kar sakta hai. Is right ko normal grant/revoke se transfer nahi kiya jata.

---

# 🪟 23. Views aur Security

Views security ka important part ho sakti hain.

Example:

Agar `STUDENT` table mein:

```text
stId
stName
email
password
cgpa
```

hai aur kisi teacher ko sirf:

```text
stId
stName
cgpa
```

dikhana hai, to ek view banaya ja sakta hai aur us view par permissions di ja sakti hain.

```sql
CREATE VIEW StudentPublic AS
SELECT stId, stName, cgpa
FROM STUDENT;
```

Phir:

```sql
GRANT SELECT ON StudentPublic TO Teacher;
```

Is tarah teacher ko poori base table dene ke bajaye limited information di ja sakti hai.

---

# 📝 24. Lecture ke Important Examples

## Example 1 – Inner Join

```sql
SELECT *
FROM COURSE c
INNER JOIN PROGRAM p
ON c.prName = p.prName;
```

**Use:** Sirf matching courses/programs.

---

## Example 2 – Left Join

```sql
SELECT *
FROM COURSE c
LEFT JOIN PROGRAM p
ON c.prName = p.prName;
```

**Use:** Har course show karo, matching program ho to uski detail bhi show karo.

---

## Example 3 – Right Join

```sql
SELECT *
FROM COURSE c
RIGHT JOIN PROGRAM p
ON c.prName = p.prName;
```

**Use:** Har program show karo, matching course ho to uski detail bhi show karo.

---

## Example 4 – Full Join

```sql
SELECT *
FROM COURSE c
FULL OUTER JOIN PROGRAM p
ON c.prName = p.prName;
```

**Use:** Dono tables ki complete information, matched + unmatched.

---

## Example 5 – Self Join

```sql
SELECT a.stName AS Student,
       b.stName AS ClassRepresentative
FROM STUDENT a
JOIN STUDENT b
ON a.cr = b.stId;
```

**Use:** Student ka CR find karna.

---

## Example 6 – Subquery

```sql
SELECT *
FROM STUDENT
WHERE cgpa = (
    SELECT MAX(cgpa)
    FROM STUDENT
);
```

**Use:** Highest CGPA wale student(s).

---

## Example 7 – GRANT

```sql
GRANT SELECT ON COURSE TO Mina;
```

**Use:** Mina ko COURSE read karne ki permission.

---

## Example 8 – GRANT with Grant Option

```sql
GRANT SELECT
ON COURSE
TO Alia
WITH GRANT OPTION;
```

**Use:** Alia read bhi kar sakti hai aur doosron ko SELECT privilege bhi de sakti hai.

---

## Example 9 – REVOKE

```sql
REVOKE SELECT
ON COURSE
FROM Alia
CASCADE;
```

**Use:** Alia se SELECT privilege wapas lena aur dependent grants par bhi effect dena.

---

# 🧠 25. Most Important Differences

## INNER JOIN vs LEFT JOIN

| INNER JOIN | LEFT JOIN |
|---|---|
| Matching rows only | Left table ki all rows |
| Unmatched left rows remove | Unmatched left rows remain |
| No matching row → no output | No matching row → NULLs |

---

## LEFT JOIN vs RIGHT JOIN

| LEFT JOIN | RIGHT JOIN |
|---|---|
| Left table ki all rows | Right table ki all rows |
| Left side important | Right side important |

---

## INNER JOIN vs FULL OUTER JOIN

| INNER | FULL |
|---|---|
| Matching rows | Matching + unmatched rows |
| Sirf common data | Dono tables ka complete coverage |

---

## GRANT vs REVOKE

| GRANT | REVOKE |
|---|---|
| Permission dena | Permission wapas lena |
| Add privilege | Remove privilege |

---

## CASCADE vs RESTRICT

| CASCADE | RESTRICT |
|---|---|
| Dependent privileges ko bhi affect kar sakta hai | Dependent effect ho to revoke reject kar sakta hai |

---

# 🎯 26. Exam ke Liye One-Page Revision

### JOIN

```text
JOIN = Do tables ko related condition ke basis par combine karna
```

### INNER JOIN

```text
Only matching rows
```

### LEFT JOIN

```text
All rows from LEFT table
```

### RIGHT JOIN

```text
All rows from RIGHT table
```

### FULL JOIN

```text
All rows from BOTH tables
```

### SEMI JOIN

```text
Matching rows of one table
```

### SELF JOIN

```text
A table joined with itself
```

### SUBQUERY

```text
Query inside another query
```

### GRANT

```text
Permission dena
```

### REVOKE

```text
Permission wapas lena
```

### WITH GRANT OPTION

```text
User apni permission doosre user ko bhi de sakta hai
```

### CASCADE

```text
Dependent grants bhi revoke ho sakti hain
```

### RESTRICT

```text
Dependent effect ho to revoke reject ho sakti hai
```

---

# ⭐ 27. Most Important SQL Patterns to Memorize

## Inner Join

```sql
SELECT *
FROM A
INNER JOIN B
ON A.common = B.common;
```

## Left Join

```sql
SELECT *
FROM A
LEFT JOIN B
ON A.common = B.common;
```

## Right Join

```sql
SELECT *
FROM A
RIGHT JOIN B
ON A.common = B.common;
```

## Full Join

```sql
SELECT *
FROM A
FULL OUTER JOIN B
ON A.common = B.common;
```

## Self Join

```sql
SELECT a.column1, b.column1
FROM TableName a
JOIN TableName b
ON a.foreignKey = b.primaryKey;
```

## Subquery

```sql
SELECT *
FROM STUDENT
WHERE cgpa = (
    SELECT MAX(cgpa)
    FROM STUDENT
);
```

## Grant

```sql
GRANT SELECT ON COURSE TO UserName;
```

## Grant Option

```sql
GRANT SELECT ON COURSE
TO UserName WITH GRANT OPTION;
```

## Revoke

```sql
REVOKE SELECT ON COURSE
FROM UserName CASCADE;
```

---

# ✅ 28. Final Quick Summary

Lecture 31 ka poora concept ek simple story se samjho:

### Tables ko combine karna ho?
➡️ **JOIN**

### Sirf matching rows chahiye?
➡️ **INNER JOIN**

### Left table ki har row chahiye?
➡️ **LEFT JOIN**

### Right table ki har row chahiye?
➡️ **RIGHT JOIN**

### Dono tables ki har row chahiye?
➡️ **FULL OUTER JOIN**

### Ek hi table ko do roles mein compare karna ho?
➡️ **SELF JOIN**

### Kisi ek table ki sirf matching rows identify karni hon?
➡️ **SEMI JOIN**

### Query ke andar doosri query ho?
➡️ **SUBQUERY**

### User ko permission deni ho?
➡️ **GRANT**

### Permission wapas leni ho?
➡️ **REVOKE**

### Permission ke saath aage permission dene ki power deni ho?
➡️ **WITH GRANT OPTION**

### Dependent permissions ko bhi remove karna ho?
➡️ **CASCADE**

### Dependent privilege issue ki wajah se revoke ko rokna ho?
➡️ **RESTRICT**

---

# 🧪 29. Practice Questions

### Q1. INNER JOIN kya hota hai?
**Answer:** Do tables ki sirf matching rows ko combine karta hai.

### Q2. LEFT JOIN kya return karta hai?
**Answer:** Left table ki saari rows aur matching right rows.

### Q3. SELF JOIN mein alias kyun use hota hai?
**Answer:** Kyun ke same table ko multiple roles/names ke saath reference karna hota hai.

### Q4. Subquery kya hoti hai?
**Answer:** Ek query ke andar embedded query.

### Q5. Subquery pehle execute hoti hai ya outer query?
**Answer:** Conceptually inner/subquery pehle evaluate hoti hai.

### Q6. GRANT ka purpose kya hai?
**Answer:** User ko privileges dena.

### Q7. REVOKE ka purpose kya hai?
**Answer:** User ki privileges withdraw karna.

### Q8. WITH GRANT OPTION kya karta hai?
**Answer:** User ko privilege doosre users ko grant karne ki permission deta hai.

### Q9. CASCADE kya karta hai?
**Answer:** Dependent grants/privileges ko bhi revoke kar sakta hai.

### Q10. FULL OUTER JOIN kya return karta hai?
**Answer:** Dono tables ki matching aur unmatched dono rows.

---

# ⭐ Exam Tip

Agar paper mein JOIN ka question aaye to sabse pehle ye 4 words yaad karo:

```text
INNER = MATCH
LEFT  = ALL LEFT
RIGHT = ALL RIGHT
FULL  = ALL BOTH
```

Aur Access Control ke liye:

```text
GRANT  = GIVE PERMISSION
REVOKE = TAKE BACK PERMISSION
CASCADE = DEPENDENTS ALSO AFFECTED
RESTRICT = REVOKE CAN BE REJECTED
```

---

# 📌 Final Takeaway

> **Lecture 31 ka main idea:** SQL JOINs tables ki related information ko combine karte hain, Subqueries ek query ke andar another query ka result use karti hain, aur GRANT/REVOKE database users ki permissions control karte hain.

**Best of luck for your paper! 🌸📚**
