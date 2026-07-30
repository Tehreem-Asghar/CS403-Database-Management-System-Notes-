# 📚 DBMS – Lecture 29
## WHERE Clause, SQL Operators & ORDER BY

> **Course:** CS403 – Database Management Systems  
> **Lecture:** 29  
> **Topic:** Data Manipulation Language (DML) – WHERE Clause  
> **Language:** Roman Urdu + English SQL  
> **Level:** Beginner Friendly

---

# 📌 Lecture Overview

Is lecture mein hum SQL ki **WHERE clause** ko detail mein samjhenge.

WHERE clause ka basic purpose hai:

> **Table mein se sirf woh rows/records select karna jo hamari condition ko satisfy karte hain.**

Is lecture ke important topics:

1. WHERE Clause
2. Search Condition
3. Comparison Operators
4. AND Operator
5. OR Operator
6. NOT Operator
7. BETWEEN Operator
8. IN Operator
9. LIKE Operator
10. `%` Wildcard
11. `_` Wildcard
12. IS NULL / IS NOT NULL
13. EXISTS
14. ANY / SOME
15. ALL
16. WHERE se Multiple Tables Join Karna
17. ORDER BY
18. ASC / DESC
19. Real-Life Examples
20. Exam Revision & Quick Summary

---

# 1. WHERE Clause Kya Hoti Hai?

SQL mein `WHERE` clause ka use table ke records ko **filter** karne ke liye hota hai.

Simple Roman Urdu mein:

> **WHERE ka matlab hai: "Sirf woh records dikhao jo meri condition puri karte hain."**

Suppose hamare paas `supplier` table hai:

| supplier_id | supplier_name | supplier_city |
|---:|---|---|
| 1 | IBM | Karachi |
| 2 | Microsoft | Lahore |
| 3 | IBM | Islamabad |
| 4 | Dell | Karachi |

Agar humein sirf IBM suppliers chahiye:

```sql
SELECT *
FROM supplier
WHERE supplier_name = 'IBM';
```

### Result

| supplier_id | supplier_name | supplier_city |
|---:|---|---|
| 1 | IBM | Karachi |
| 3 | IBM | Islamabad |

SQL ne table ki rows check ki aur sirf woh rows select ki jin mein:

```text
supplier_name = 'IBM'
```

---

# 2. WHERE Optional Hoti Hai

`WHERE` clause **optional** hoti hai.

Agar WHERE nahi lagayenge to query normally table ki saari rows return karegi.

## Without WHERE

```sql
SELECT *
FROM supplier;
```

Is query mein supplier table ke **all records** display honge.

## With WHERE

```sql
SELECT *
FROM supplier
WHERE supplier_city = 'Karachi';
```

Ab sirf Karachi ke suppliers display honge.

### Easy Formula

```text
SELECT  → Kya data chahiye?
FROM    → Kis table se chahiye?
WHERE   → Kin records ki zaroorat hai?
```

---

# 3. WHERE Ka Basic Syntax

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Example

```sql
SELECT supplier_name, supplier_city
FROM supplier
WHERE supplier_city = 'Karachi';
```

Meaning:

> Supplier table se supplier name aur city show karo, lekin sirf un suppliers ki jinki city Karachi hai.

---

# 4. Search Condition

WHERE ke andar jo condition likhi jati hai usay **search condition** kehte hain.

Example:

```sql
WHERE supplier_city = 'Karachi'
```

Yahan:

```text
supplier_city = 'Karachi'
```

search condition hai.

SQL har row ko check karti hai:

```text
Condition TRUE  → Row select hogi ✅
Condition FALSE → Row select nahi hogi ❌
```

---

# 5. Comparison Operators

WHERE clause mein comparison karne ke liye different operators use hote hain.

| Operator | Meaning |
|---|---|
| `=` | Equal to |
| `<>` | Not equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `>=` | Greater than or equal |
| `<` | Less than |
| `<=` | Less than or equal |

---

# 6. Equal To `=`

`=` ka matlab hai **barabar**.

```sql
SELECT *
FROM supplier
WHERE supplier_name = 'IBM';
```

Meaning:

> Sirf woh suppliers show karo jinka naam IBM hai.

---

# 7. Not Equal `<>` / `!=`

`<>` ya `!=` ka matlab hai **barabar nahi**.

```sql
SELECT *
FROM supplier
WHERE supplier_city <> 'Karachi';
```

Meaning:

> Karachi ke ilawa baqi cities ke suppliers show karo.

Another example:

```sql
SELECT *
FROM student
WHERE marks != 50;
```

Meaning:

> Jin students ke marks 50 nahi hain unko show karo.

---

# 8. Greater Than `>`

`>` ka matlab hai **se bara**.

```sql
SELECT *
FROM student
WHERE marks > 80;
```

Meaning:

> Sirf un students ko show karo jinke marks 80 se zyada hain.

Example values:

```text
70
75
81
90
95
```

Result:

```text
81
90
95
```

---

# 9. Greater Than or Equal `>=`

`>=` ka matlab hai:

> **bara ya barabar**

```sql
SELECT *
FROM student
WHERE marks >= 80;
```

Is mein 80 bhi include hoga.

```text
80 ✅
81 ✅
90 ✅
```

---

# 10. Less Than `<`

`<` ka matlab hai **se chota**.

```sql
SELECT *
FROM student
WHERE marks < 50;
```

Meaning:

> 50 se kam marks wale students show karo.

---

# 11. Less Than or Equal `<=`

`<=` ka matlab hai:

> **chota ya barabar**

```sql
SELECT *
FROM student
WHERE marks <= 50;
```

Is mein 50 bhi include hoga.

```text
49 ✅
50 ✅
51 ❌
```

---

# 12. AND Operator

`AND` ka matlab hai:

> **Dono conditions true honi chahiye.**

Example:

```sql
SELECT *
FROM supplier
WHERE supplier_name = 'IBM'
AND supplier_city = 'Karachi';
```

Is query mein:

1. Supplier ka naam IBM hona chahiye.
2. Supplier ki city Karachi honi chahiye.

Dono conditions satisfy hongi tab row select hogi.

### Example Table

| supplier_name | supplier_city |
|---|---|
| IBM | Karachi |
| IBM | Lahore |
| Dell | Karachi |
| Microsoft | Lahore |

### Result

| supplier_name | supplier_city |
|---|---|
| IBM | Karachi |

---

# 13. OR Operator

`OR` ka matlab hai:

> **Kam az kam ek condition true honi chahiye.**

Example:

```sql
SELECT supplier_id
FROM supplier
WHERE supplier_name = 'IBM'
OR supplier_city = 'Karachi';
```

Meaning:

> Supplier IBM ho **ya** Karachi mein ho.

### Example Table

| supplier_id | supplier_name | supplier_city |
|---:|---|---|
| 1 | IBM | Karachi |
| 2 | IBM | Lahore |
| 3 | Dell | Karachi |
| 4 | Microsoft | Lahore |

### Result

```text
1
2
3
```

Reason:

- Row 1 → IBM bhi hai aur Karachi bhi ✅
- Row 2 → IBM hai ✅
- Row 3 → Karachi hai ✅
- Row 4 → IBM bhi nahi aur Karachi bhi nahi ❌

---

# 14. NOT Operator

`NOT` condition ko **reverse** karta hai.

Example:

```sql
SELECT *
FROM course
WHERE NOT (prName = 'MCS');
```

Meaning:

> MCS ke ilawa baqi programs ke courses show karo.

### Example

Agar table mein:

| crCode | crName | prName |
|---|---|---|
| CS101 | Programming | BCS |
| CS201 | Database | MCS |
| CS301 | AI | MCS |
| ENG101 | English | BCS |

To result:

| crCode | crName | prName |
|---|---|---|
| CS101 | Programming | BCS |
| ENG101 | English | BCS |

### Easy Rule

```text
WHERE condition
        ↓
    normal result

WHERE NOT condition
        ↓
    reverse result
```

---

# 15. MCS Program ke Courses

Lecture ka example:

> **Display all courses of the MCS program**

```sql
SELECT crCode, crName, prName
FROM course
WHERE prName = 'MCS';
```

SQL rows ko check karegi aur sirf `prName = 'MCS'` wali rows display karegi.

---

# 16. MCS ke Ilawa Courses

Question:

> **List the course names offered to programs other than MCS.**

```sql
SELECT crCode, crName, prName
FROM course
WHERE NOT (prName = 'MCS');
```

Yahan `NOT` MCS condition ko reverse kar raha hai.

Alternative:

```sql
SELECT crCode, crName, prName
FROM course
WHERE prName <> 'MCS';
```

Dono ka basic purpose MCS ke ilawa records lana hai.

---

# 17. BETWEEN Operator

`BETWEEN` ka use values ko **specific range** mein check karne ke liye hota hai.

### Syntax

```sql
SELECT columns
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### Important

`BETWEEN` mein **starting aur ending values dono include hoti hain**.

Example:

```text
BETWEEN 10 AND 50
```

means:

```text
10 ≤ value ≤ 50
```

Yani 10 aur 50 dono include hain.

---

# 18. BETWEEN ka Example

```sql
SELECT *
FROM suppliers
WHERE supplier_id BETWEEN 10 AND 50;
```

Meaning:

> Supplier ID 10 se 50 ke darmiyan wale suppliers show karo.

Include honge:

```text
10 ✅
20 ✅
30 ✅
40 ✅
50 ✅
```

Exclude honge:

```text
9 ❌
51 ❌
```

---

# 19. BETWEEN with Marks

```sql
SELECT *
FROM student
WHERE marks BETWEEN 60 AND 80;
```

Meaning:

> 60 se 80 tak marks wale students show karo.

Values:

```text
59 ❌
60 ✅
65 ✅
70 ✅
75 ✅
80 ✅
81 ❌
```

---

# 20. NOT BETWEEN

Range ke andar ki values ke bajaye range ke **bahar** wali values chahiye hon to `NOT BETWEEN` use karte hain.

```sql
SELECT *
FROM supplier
WHERE supplier_id NOT BETWEEN 10 AND 50;
```

Meaning:

> Supplier IDs 10 se 50 ke ilawa baqi IDs show karo.

---

# 21. IN Operator

`IN` ka use ek column ko **multiple values ki list** ke saath compare karne ke liye hota hai.

Simple Roman Urdu:

> Jab ek field ke liye kai possible values hon, to `IN` use kar sakte hain.

### Syntax

```sql
SELECT columns
FROM table_name
WHERE column_name IN (value1, value2, value3);
```

---

# 22. IN Example

Lecture ka example:

```sql
SELECT crName, prName
FROM course
WHERE prName IN ('MCS', 'BCS');
```

Meaning:

> Woh courses show karo jo MCS ya BCS program ke hain.

---

# 23. IN aur OR Same Result De Sakte Hain

Ye query:

```sql
SELECT crName, prName
FROM course
WHERE prName IN ('MCS', 'BCS');
```

Aur ye:

```sql
SELECT crName, prName
FROM course
WHERE prName = 'MCS'
OR prName = 'BCS';
```

Dono ka result same ho sakta hai.

### Easy Concept

```text
IN = multiple OR conditions ka short aur clean form
```

### Example

Instead of:

```sql
WHERE city = 'Karachi'
OR city = 'Lahore'
OR city = 'Islamabad'
```

Use:

```sql
WHERE city IN ('Karachi', 'Lahore', 'Islamabad')
```

---

# 24. NOT IN

Agar humein list ke **ilawa** values chahiye hon:

```sql
SELECT *
FROM course
WHERE prName NOT IN ('MCS', 'BCS');
```

Meaning:

> MCS aur BCS ke ilawa baqi programs ke records show karo.

---

# 25. LIKE Operator

`LIKE` ka use **pattern matching** ke liye hota hai.

Simple Roman Urdu:

> Jab humein exact value nahi pata, lekin value ka pattern pata hai, to `LIKE` use karte hain.

Examples:

- Naam A se start hota hai.
- Naam mein `Ali` kahin bhi hai.
- Program ka naam `CS` par end hota hai.

---

# 26. LIKE ke Wildcards

LIKE ke saath commonly do important wildcards use hote hain:

| Wildcard | Meaning |
|---|---|
| `%` | Zero, one ya multiple characters |
| `_` | Exactly one character |

---

# 27. `%` Wildcard

`%` ka matlab:

> **Koi bhi number of characters, including zero.**

## Example 1 – Start With

```sql
SELECT *
FROM student
WHERE name LIKE 'Ali%';
```

Meaning:

> Naam `Ali` se start hona chahiye.

Possible matches:

```text
Ali
Aliya
Alina
Ali Raza
```

---

# 28. `%` End With

```sql
SELECT *
FROM student
WHERE name LIKE '%Ali';
```

Meaning:

> Naam `Ali` par end hona chahiye.

Possible examples:

```text
Ali
Ahmed Ali
Muhammad Ali
```

---

# 29. `%` Anywhere

```sql
SELECT *
FROM student
WHERE name LIKE '%Ali%';
```

Meaning:

> Naam mein `Ali` kahin bhi ho sakta hai.

Possible examples:

```text
Ali
Aliya
Muhammad Ali
Alina
```

---

# 30. `_` Wildcard

`_` ka matlab:

> **Exactly one character**

Example:

```sql
SELECT *
FROM student
WHERE name LIKE 'A_i';
```

Pattern:

```text
A + one character + i
```

Examples:

```text
Ali ✅
Ami ✅
Axi ✅
```

Lekin:

```text
Abhi ❌
```

kyun ke `Abhi` mein 4 characters hain.

---

# 31. Lecture ka LIKE Example

Question:

> **Display the names and credits of CS programs.**

```sql
SELECT crName, crCrdts, prName
FROM course
WHERE prName LIKE '%CS';
```

Yahan:

```text
%CS
```

ka matlab hai:

> Program name ke end mein `CS` hona chahiye.

Examples:

```text
BCS ✅
MCS ✅
BSCS ✅
```

---

# 32. IS NULL

`NULL` ka matlab hota hai ke kisi field mein **value missing / unknown** hai.

Example:

```sql
SELECT *
FROM student
WHERE phone IS NULL;
```

Meaning:

> Un students ko show karo jinka phone number available nahi hai.

### Important

NULL check karne ke liye normally:

```sql
WHERE phone = NULL
```

nahi likhte.

Correct:

```sql
WHERE phone IS NULL
```

---

# 33. IS NOT NULL

Jahan value missing nahi hai:

```sql
SELECT *
FROM student
WHERE phone IS NOT NULL;
```

Meaning:

> Sirf un students ko show karo jinka phone number available hai.

### Easy Difference

```text
IS NULL
→ value missing

IS NOT NULL
→ value available
```

---

# 34. EXISTS

`EXISTS` ka use check karne ke liye hota hai ke subquery **kam az kam ek row return karti hai ya nahi**.

Ye thora advanced operator hai.

### Example

```sql
SELECT s.supplier_name
FROM supplier s
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.supplier_id = s.supplier_id
);
```

Meaning:

> Sirf un suppliers ke names show karo jinke orders exist karte hain.

Simple question:

```text
"Kya is supplier ka koi related order hai?"
```

Agar answer YES ho to supplier select ho jayega.

---

# 35. ANY / SOME

`ANY` ya `SOME` ka use subquery ki values ke saath comparison mein hota hai.

Simple meaning:

> **Kam az kam ek value ke saath condition true honi chahiye.**

Conceptual example:

```sql
WHERE salary > ANY (
    SELECT salary
    FROM employee
    WHERE department = 'IT'
);
```

Meaning:

> Salary IT department ki kam az kam ek salary se zyada ho.

### Remember

```text
ANY = at least one
SOME = at least one
```

---

# 36. ALL

`ALL` ka matlab hai:

> Condition ko subquery ki **har value** ke saath true hona chahiye.

Example:

```sql
WHERE salary > ALL (
    SELECT salary
    FROM employee
    WHERE department = 'IT'
);
```

Meaning:

> Salary IT department ki **har salary** se zyada honi chahiye.

### Easy Difference

```text
ANY → kam az kam ek
ALL → sab
```

---

# 37. WHERE se Multiple Tables Join Karna

WHERE clause ka ek important use multiple tables ko join karna bhi hai.

Lecture ka example:

```sql
SELECT supplier.supplier_name, orders.order_id
FROM supplier, orders
WHERE supplier.supplier_id = orders.supplier_id
AND supplier.supplier_city = 'Karachi';
```

Is query mein do tables hain:

```text
supplier
orders
```

Unko `supplier_id` ke through connect kiya gaya hai.

---

# 38. JOIN Example ko Step-by-Step Samjhein

## Supplier Table

| supplier_id | supplier_name | supplier_city |
|---:|---|---|
| 1 | IBM | Karachi |
| 2 | Dell | Lahore |
| 3 | HP | Karachi |

## Orders Table

| order_id | supplier_id |
|---:|---:|
| 101 | 1 |
| 102 | 2 |
| 103 | 1 |
| 104 | 3 |

Query:

```sql
SELECT supplier.supplier_name, orders.order_id
FROM supplier, orders
WHERE supplier.supplier_id = orders.supplier_id
AND supplier.supplier_city = 'Karachi';
```

### Result

| supplier_name | order_id |
|---|---:|
| IBM | 101 |
| IBM | 103 |
| HP | 104 |

### Kya ho raha hai?

Condition 1:

```sql
supplier.supplier_id = orders.supplier_id
```

Matlab:

> Supplier aur order ka supplier ID same ho.

Condition 2:

```sql
supplier.supplier_city = 'Karachi'
```

Matlab:

> Supplier Karachi ka ho.

---

# 39. Multiple Conditions ko Combine Karna

Hum WHERE mein multiple operators combine kar sakte hain.

Example:

```sql
SELECT *
FROM student
WHERE marks >= 80
AND city = 'Karachi'
AND program = 'BSCS';
```

Meaning:

> Karachi ke BSCS students jo 80 ya us se zyada marks rakhte hain.

---

# 40. AND vs OR – Important Difference

## AND

```sql
WHERE city = 'Karachi'
AND marks > 80;
```

Dono conditions true honi chahiye.

```text
Condition 1 ✅
Condition 2 ✅
Final ✅
```

Agar koi ek false:

```text
Condition 1 ✅
Condition 2 ❌
Final ❌
```

---

## OR

```sql
WHERE city = 'Karachi'
OR city = 'Lahore';
```

Koi ek condition true ho to row select ho sakti hai.

```text
Karachi ✅
Lahore ✅
Islamabad ❌
```

---

# 41. Parentheses ke Saath Conditions

Complex conditions mein parentheses useful hoti hain.

Example:

```sql
SELECT *
FROM student
WHERE (city = 'Karachi' OR city = 'Lahore')
AND marks >= 80;
```

Meaning:

> Karachi ya Lahore ke students mein se sirf unko show karo jinke marks 80 ya us se zyada hain.

Parentheses se humein clear hota hai ke pehle kis condition ka group ban raha hai.

---

# 42. ORDER BY Clause

`ORDER BY` ka use result ko **sort / arrange** karne ke liye hota hai.

Important:

> Lecture ke mutabiq `ORDER BY` sirf SELECT statement ke saath use hota hai.

### Syntax

```sql
SELECT columns
FROM table_name
WHERE condition
ORDER BY column_name ASC;
```

Ya:

```sql
SELECT columns
FROM table_name
WHERE condition
ORDER BY column_name DESC;
```

---

# 43. ASC – Ascending Order

`ASC` ka matlab:

> **Choti value se bari value ki taraf**

Numbers:

```text
10
20
30
40
50
```

Marks:

```text
55
68
72
81
95
```

Example:

```sql
SELECT *
FROM student
ORDER BY marks ASC;
```

---

# 44. DESC – Descending Order

`DESC` ka matlab:

> **Bari value se choti value ki taraf**

Example:

```sql
SELECT *
FROM student
ORDER BY marks DESC;
```

Result:

```text
95
90
85
80
70
```

---

# 45. ASC Default Hota Hai

Agar `ASC` ya `DESC` nahi likha:

```sql
SELECT *
FROM student
ORDER BY marks;
```

To normally ascending order assume kiya jata hai.

Yani:

```sql
ORDER BY marks
```

ko normally:

```sql
ORDER BY marks ASC
```

samjha ja sakta hai.

---

# 46. WHERE + ORDER BY Together

WHERE filtering karta hai aur ORDER BY sorting.

Example:

```sql
SELECT name, marks, city
FROM student
WHERE city = 'Karachi'
ORDER BY marks DESC;
```

### Step 1

```sql
WHERE city = 'Karachi'
```

Sirf Karachi ke students select honge.

### Step 2

```sql
ORDER BY marks DESC
```

Selected students highest marks se lowest marks ke order mein aayenge.

---

# 47. Complete Real-Life Student Table

Suppose:

| id | name | marks | city | program |
|---:|---|---:|---|---|
| 1 | Ali | 85 | Karachi | BCS |
| 2 | Sara | 72 | Lahore | MCS |
| 3 | Ahmed | 91 | Karachi | MCS |
| 4 | Hina | 65 | Islamabad | BCS |
| 5 | Usman | 88 | Karachi | BCS |

---

## Example 1 – Karachi Students

```sql
SELECT *
FROM student
WHERE city = 'Karachi';
```

Result:

| id | name | marks | city | program |
|---:|---|---:|---|---|
| 1 | Ali | 85 | Karachi | BCS |
| 3 | Ahmed | 91 | Karachi | MCS |
| 5 | Usman | 88 | Karachi | BCS |

---

## Example 2 – Marks Greater Than 80

```sql
SELECT *
FROM student
WHERE marks > 80;
```

Result:

| name | marks |
|---|---:|
| Ali | 85 |
| Ahmed | 91 |
| Usman | 88 |

---

## Example 3 – Karachi + 80 or More Marks

```sql
SELECT *
FROM student
WHERE city = 'Karachi'
AND marks >= 80;
```

Result:

| name | marks | city |
|---|---:|---|
| Ali | 85 | Karachi |
| Ahmed | 91 | Karachi |
| Usman | 88 | Karachi |

---

## Example 4 – BCS ya MCS

```sql
SELECT *
FROM student
WHERE program IN ('BCS', 'MCS');
```

---

## Example 5 – 70 to 90 Marks

```sql
SELECT *
FROM student
WHERE marks BETWEEN 70 AND 90;
```

---

## Example 6 – Name A se Start

```sql
SELECT *
FROM student
WHERE name LIKE 'A%';
```

Result:

| name |
|---|
| Ali |
| Ahmed |

---

## Example 7 – Karachi ke Ilawa

```sql
SELECT *
FROM student
WHERE city <> 'Karachi';
```

---

## Example 8 – Highest Marks First

```sql
SELECT *
FROM student
ORDER BY marks DESC;
```

Result order:

```text
Ahmed  → 91
Usman  → 88
Ali    → 85
Sara   → 72
Hina   → 65
```

---

## Example 9 – Karachi Students Highest Marks First

```sql
SELECT name, marks
FROM student
WHERE city = 'Karachi'
ORDER BY marks DESC;
```

Result:

| name | marks |
|---|---:|
| Ahmed | 91 |
| Usman | 88 |
| Ali | 85 |

---

# 48. Course Table – Lecture Style Example

Assume `course` table:

| crCode | crName | crCrdts | prName |
|---|---|---:|---|
| CS101 | Programming | 3 | BCS |
| CS201 | Database | 3 | MCS |
| CS301 | AI | 3 | MCS |
| CS401 | Web Engineering | 3 | BSCS |
| ENG101 | English | 3 | BCS |

---

## All MCS Courses

```sql
SELECT crCode, crName, prName
FROM course
WHERE prName = 'MCS';
```

---

## Courses Other Than MCS

```sql
SELECT crCode, crName, prName
FROM course
WHERE prName <> 'MCS';
```

---

## BCS and MCS Courses

```sql
SELECT crName, prName
FROM course
WHERE prName IN ('BCS', 'MCS');
```

---

## All CS Programs

```sql
SELECT crName, crCrdts, prName
FROM course
WHERE prName LIKE '%CS';
```

---

# 49. WHERE ka Execution Idea

Simple learning level par WHERE ko is tarah samjhein:

```text
Table
  ↓
Rows ko check karo
  ↓
WHERE condition apply karo
  ↓
TRUE rows select karo
  ↓
Result display karo
```

Example:

```sql
SELECT name, marks
FROM student
WHERE marks >= 80;
```

Conceptually:

```text
Ali    85  → TRUE  → Select ✅
Sara   72  → FALSE → Ignore ❌
Ahmed  91  → TRUE  → Select ✅
Hina   65  → FALSE → Ignore ❌
Usman  88  → TRUE  → Select ✅
```

---

# 50. Common Mistakes

## Mistake 1 – Text Value ke Quotes Bhool Jana

Wrong:

```sql
WHERE city = Karachi;
```

Correct:

```sql
WHERE city = 'Karachi';
```

Text values ko normally quotes mein likha jata hai.

---

## Mistake 2 – NULL ke saath `=`

Wrong:

```sql
WHERE phone = NULL;
```

Correct:

```sql
WHERE phone IS NULL;
```

---

## Mistake 3 – BETWEEN ka Concept

```sql
WHERE marks BETWEEN 60 AND 80;
```

Is mein 60 aur 80 **dono included** hain.

---

## Mistake 4 – IN mein Parentheses

Correct:

```sql
WHERE city IN ('Karachi', 'Lahore');
```

---

## Mistake 5 – LIKE aur `%`

Agar naam A se start hona chahiye:

```sql
WHERE name LIKE 'A%';
```

Agar naam A par end hona chahiye:

```sql
WHERE name LIKE '%A';
```

Agar kahin bhi A ho:

```sql
WHERE name LIKE '%A%';
```

---

# 51. Quick Comparison – Operators

| Requirement | Operator | Example |
|---|---|---|
| Exact value | `=` | `marks = 80` |
| Value different ho | `<>` | `marks <> 80` |
| Greater | `>` | `marks > 80` |
| Greater/equal | `>=` | `marks >= 80` |
| Less | `<` | `marks < 80` |
| Less/equal | `<=` | `marks <= 80` |
| Both conditions | `AND` | `city='Karachi' AND marks>80` |
| Any condition | `OR` | `city='Karachi' OR city='Lahore'` |
| Reverse | `NOT` | `NOT city='Karachi'` |
| Range | `BETWEEN` | `marks BETWEEN 60 AND 80` |
| Multiple values | `IN` | `city IN ('Karachi','Lahore')` |
| Pattern | `LIKE` | `name LIKE 'A%'` |
| Missing | `IS NULL` | `phone IS NULL` |
| Not missing | `IS NOT NULL` | `phone IS NOT NULL` |
| Existence | `EXISTS` | `EXISTS (...)` |
| At least one | `ANY` | `> ANY (...)` |
| Every value | `ALL` | `> ALL (...)` |

---

# 52. LIKE Wildcard Quick Revision

| Pattern | Meaning | Example |
|---|---|---|
| `'A%'` | A se start | Ali, Ahmed |
| `'%A'` | A par end | Hina, Sara? |
| `'%A%'` | A kahin bhi ho | Ali, Sara, Ahmed |
| `'A_i'` | A + one character + i | Ali, Ami |

> **Note:** Case sensitivity aur wildcard behavior database system ke mutabiq vary kar sakta hai.

---

# 53. Most Important SQL Queries

## 1. Exact Match

```sql
SELECT *
FROM supplier
WHERE supplier_name = 'IBM';
```

## 2. Multiple Conditions

```sql
SELECT *
FROM supplier
WHERE supplier_name = 'IBM'
AND supplier_city = 'Karachi';
```

## 3. OR

```sql
SELECT *
FROM supplier
WHERE supplier_name = 'IBM'
OR supplier_city = 'Karachi';
```

## 4. NOT

```sql
SELECT *
FROM course
WHERE NOT (prName = 'MCS');
```

## 5. BETWEEN

```sql
SELECT *
FROM supplier
WHERE supplier_id BETWEEN 10 AND 50;
```

## 6. NOT BETWEEN

```sql
SELECT *
FROM supplier
WHERE supplier_id NOT BETWEEN 10 AND 50;
```

## 7. IN

```sql
SELECT *
FROM course
WHERE prName IN ('MCS', 'BCS');
```

## 8. NOT IN

```sql
SELECT *
FROM course
WHERE prName NOT IN ('MCS', 'BCS');
```

## 9. LIKE

```sql
SELECT *
FROM course
WHERE prName LIKE '%CS';
```

## 10. IS NULL

```sql
SELECT *
FROM student
WHERE phone IS NULL;
```

## 11. IS NOT NULL

```sql
SELECT *
FROM student
WHERE phone IS NOT NULL;
```

## 12. ORDER BY ASC

```sql
SELECT *
FROM student
ORDER BY marks ASC;
```

## 13. ORDER BY DESC

```sql
SELECT *
FROM student
ORDER BY marks DESC;
```

## 14. WHERE + ORDER BY

```sql
SELECT name, marks
FROM student
WHERE marks >= 80
ORDER BY marks DESC;
```

---

# 54. Exam Point of View

### Q: WHERE clause kya karti hai?

**Answer:**

> WHERE clause SQL query ke result ko filter karti hai aur sirf woh rows return karti hai jo specified search condition ko satisfy karti hain.

---

### Q: BETWEEN kya karta hai?

**Answer:**

> BETWEEN kisi value ko specified range mein check karta hai. Starting aur ending values normally include hoti hain.

---

### Q: IN ka purpose kya hai?

**Answer:**

> IN ek column ko multiple values ki list ke saath compare karta hai aur multiple OR conditions ko short aur readable banata hai.

---

### Q: LIKE kya karta hai?

**Answer:**

> LIKE pattern matching ke liye use hota hai aur `%` aur `_` jaise wildcards ke through partial matching allow karta hai.

---

### Q: `%` aur `_` mein difference?

**Answer:**

```text
% = zero ya multiple characters
_ = exactly one character
```

---

### Q: ORDER BY kya karta hai?

**Answer:**

> ORDER BY query ke result ko specified column ke according sort karta hai.

---

### Q: ASC aur DESC kya hain?

```text
ASC  = Ascending order
DESC = Descending order
```

---

# 55. One-Line Memory Tricks 🧠

```text
WHERE   = Filter
AND     = Dono
OR      = Koi ek
NOT     = Reverse
BETWEEN = Range
IN      = List
LIKE    = Pattern
%       = Many characters
_       = One character
NULL    = Missing value
EXISTS  = Record exist karta hai?
ANY     = At least one
ALL     = Every one
ORDER BY = Sort
ASC     = Small → Large
DESC    = Large → Small
```

---

# 56. Final Concept Map

```text
SQL SELECT
    |
    +-- WHERE
    |    |
    |    +-- Comparison Operators
    |    |    +-- =
    |    |    +-- <>
    |    |    +-- !=
    |    |    +-- >
    |    |    +-- >=
    |    |    +-- <
    |    |    +-- <=
    |    |
    |    +-- Logical Operators
    |    |    +-- AND
    |    |    +-- OR
    |    |    +-- NOT
    |    |
    |    +-- Special Operators
    |         +-- BETWEEN
    |         +-- IN
    |         +-- LIKE
    |         +-- IS NULL
    |         +-- IS NOT NULL
    |         +-- EXISTS
    |         +-- ANY / SOME
    |         +-- ALL
    |
    +-- ORDER BY
         +-- ASC
         +-- DESC
```

---

# ⭐ Final Summary

Is lecture ka sab se important concept **WHERE clause** hai.

WHERE ka basic purpose:

> **Required rows ko filter karna.**

Examples:

```sql
-- Exact value
WHERE city = 'Karachi'

-- Multiple conditions
WHERE city = 'Karachi' AND marks >= 80

-- Either condition
WHERE city = 'Karachi' OR city = 'Lahore'

-- Reverse
WHERE NOT (program = 'MCS')

-- Range
WHERE marks BETWEEN 60 AND 80

-- List
WHERE city IN ('Karachi', 'Lahore', 'Islamabad')

-- Pattern
WHERE name LIKE 'A%'

-- Missing value
WHERE phone IS NULL
```

Aur result ko arrange karne ke liye:

```sql
ORDER BY marks ASC;
```

ya:

```sql
ORDER BY marks DESC;
```

### ✅ Sab se important formula

```text
SELECT → kya chahiye
FROM → kahan se chahiye
WHERE → kaun se records chahiye
ORDER BY → kis order mein chahiye
```

### Complete Example

```sql
SELECT name, marks, city
FROM student
WHERE city IN ('Karachi', 'Lahore')
AND marks >= 80
ORDER BY marks DESC;
```

Roman Urdu mein:

> **Student ka name, marks aur city show karo. Sirf Karachi ya Lahore ke un students ko select karo jinke marks 80 ya us se zyada hain, aur result ko highest marks se lowest marks ki taraf arrange karo.**

---

# 📖 End of Lecture 29

**Topic Covered:** WHERE Clause + Operators + ORDER BY  
**Main Skill:** SQL mein data ko filter aur sort karna  
**Most Important Operators:** `=`, `AND`, `OR`, `NOT`, `BETWEEN`, `IN`, `LIKE`, `IS NULL`  
**Sorting:** `ORDER BY ASC/DESC`
