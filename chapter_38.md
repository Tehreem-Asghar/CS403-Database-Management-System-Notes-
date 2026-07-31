# Lecture 38 — Database Indexes
## Detailed Notes with Real-Life Examples

> **Course:** Database Management Systems (DBMS)  
> **Topic:** Indexes, Clustered/Non-Clustered, Dense/Sparse, Primary/Secondary, Multi-Level and Composite Indexes  
> **Purpose:** Exam preparation + concept understanding

---

# 1. What is an Index?

Database mein **Index** ek special data structure hota hai jo records ko **quickly search aur retrieve** karne mein help karta hai.

### Simple Roman Urdu Explanation

Agar database mein 1,000,000 records hain aur humein sirf ek record find karna hai, to har record ko one-by-one check karna bohat slow hoga.

Index ek **shortcut** provide karta hai.

### Real-Life Example: Telephone Directory

Agar tumhein telephone directory mein `Ahmed` ka number dhoondna ho, to tum A se Z tak poori directory nahi parhti.

Tum directly **A** section mein jati ho.

Database index bhi isi principle par kaam karta hai.

```text
Without Index:

Record 1
   ↓
Record 2
   ↓
Record 3
   ↓
Record 4
   ↓
...
Required Record
```

With index:

```text
Index
  ↓
Required Record
```

### Main Purpose

- Search speed increase karna
- Disk I/O reduce karna
- Query performance improve karna
- Large files mein records efficiently find karna

---

# 2. Ordered Indices

**Ordered index** mein index entries kisi order mein arranged hoti hain, jaise:

```text
101
102
103
104
105
```

Agar file ke records bhi isi order mein stored hain, to is ordering ko **primary/clustering order** kaha ja sakta hai.

### Important Point

Primary index ka search key **usually primary key hota hai**, lekin **zaroori nahi**.

Yani:

```text
Primary Index Search Key ≠ Always Primary Key
```

---

# 3. Primary Index / Clustering Index

Agar file records kisi search key ke order mein physically/sequentially stored hai aur index bhi usi ordering ko represent karta hai, to isay **primary index** ya **clustering index** kaha jata hai.

### Example

Employee data:

```text
Emp_ID   Name
101      Ali
102      Sara
103      Hina
104      Ahmed
```

Agar records `Emp_ID` ke order mein stored hain:

```text
101 → 102 → 103 → 104
```

to `Emp_ID` par primary/clustering index banaya ja sakta hai.

### Easy Definition

> **Primary/Clustering Index = file ki physical/sequential ordering wali search key par index.**

---

# 4. Clustered Index

## Definition

A **clustered index** data rows ki storage/order ko determine karta hai.

Yani indexed key ke according table ka data physically organized hota hai.

### Real-Life Example: Telephone Directory

Telephone directory:

```text
Ahmed
Ali
Aslam
Bilal
Hamza
```

Last name/first name ke order mein arranged hai.

Isi tarah clustered index data ko indexed value ke order mein arrange karta hai.

---

# 5. Why is Clustered Index Fast?

Suppose table date ke according clustered hai:

```text
2026-01-01
2026-01-02
2026-01-03
2026-01-04
2026-01-05
...
```

Query:

```sql
SELECT *
FROM Orders
WHERE OrderDate BETWEEN '2026-01-02' AND '2026-01-04';
```

Database pehle `2026-01-02` find karega aur phir adjacent records read karta jayega.

### Benefit

Range queries bohat efficient ho sakti hain.

### Common Uses

- Date ranges
- Employee IDs
- Sequential numbers
- Frequently sorted columns

---

# 6. One Clustered Index per Table

Ek table ke data ko physically ek hi main order mein organize kiya ja sakta hai.

Isliye generally:

```text
One table → One clustered index
```

Lekin clustered index **multiple columns** par bhi ho sakta hai.

Isay **composite clustered index** kehte hain.

Example:

```text
(last_name, first_name)
```

---

# 7. Composite Clustered Index

Suppose employees:

```text
Last Name   First Name
Ahmed       Ali
Ahmed       Sara
Khan        Hina
Khan        Umar
```

Agar table `(last_name, first_name)` ke order mein clustered hai, to records us order mein physically arranged honge.

### Important

Composite key:

```text
(last_name, first_name)
```

Matlab index mein ek se zyada columns use ho rahi hain.

---

# 8. Non-Clustered Index

## Definition

**Non-clustered index** mein actual table rows indexed key ke order mein physically stored nahi hotin.

Index alag hota hai aur usmein actual data tak pohanchne ke liye **pointer/row locator** hota hai.

### Simple Example

Suppose table physically `Emp_ID` ke order mein hai:

```text
Emp_ID   Name
101      Ali
102      Sara
103      Ali
104      Hina
```

Agar `Name` par non-clustered index banaya:

```text
Ali  → Row 101
Ali  → Row 103
Hina → Row 104
Sara → Row 102
```

Index mein naam sorted ho sakte hain, lekin table rows physically `Emp_ID` order mein hi hain.

---

# 9. Clustered vs Non-Clustered Index

| Clustered Index | Non-Clustered Index |
|---|---|
| Data physically indexed order mein stored hota hai | Data physically indexed order mein zaroori nahi |
| Table ki storage order determine karta hai | Separate index structure hota hai |
| Usually one per table | Multiple non-clustered indexes possible |
| Range queries ke liye very useful | Specific search conditions ke liye useful |
| Actual data/index structure closely connected | Leaf entries data tak pointers/locators rakhti hain |

### Memory Trick

> **Clustered = Data ka order**  
> **Non-Clustered = Data se separate index + pointer**

---

# 10. Dense Index

## Definition

**Dense index** mein file ke **har search-key value** ke liye index entry hoti hai.

Example data:

```text
101 Ali
102 Sara
103 Hina
104 Ahmed
```

Dense index:

```text
101 → Record 101
102 → Record 102
103 → Record 103
104 → Record 104
```

Har search-key value ki index entry available hai.

---

# 11. Advantages of Dense Index

### Benefit

Search fast hoti hai because exact search-key entry mil jati hai.

### Disadvantage

Index ka size large hota hai.

Agar:

```text
1,000,000 records
```

hain to dense index mein bohat sari entries ho sakti hain.

### Maintenance

Insert/delete ke waqt index ko zyada update karna pad sakta hai.

---

# 12. Sparse Index

## Definition

**Sparse index** mein har record ke liye index entry nahi hoti.

Sirf kuch selected records/keys ki entries hoti hain.

Example:

Data:

```text
101
102
103
104
105
106
107
108
```

Sparse index:

```text
101 → Block 1
105 → Block 2
```

Agar humein `107` chahiye:

```text
Sparse Index
    |
    | 105
    v
Block 2
105
106
107  ← Required Record
108
```

Database pehle `105` wali index entry locate karega, phir us block se sequentially aage search karega.

---

# 13. Dense vs Sparse Index

| Dense | Sparse |
|---|---|
| Har search-key value ki entry | Sirf kuch entries |
| Faster lookup | Relatively slower lookup |
| More space required | Less space required |
| Maintenance zyada | Maintenance comparatively kam |
| Large index | Small index |

### Easy Memory Trick

> **Dense = Detailed**  
> **Sparse = Selected**

---

# 14. Sparse Index with One Entry per Block

Ek practical compromise hota hai:

> **Har block ke liye ek sparse index entry.**

Example:

```text
Index:
101 → Block 1
201 → Block 2
301 → Block 3
```

Har block mein multiple records hain.

### Why useful?

Database systems mein disk se block ko main memory mein lana expensive hota hai.

Agar index humein directly correct block tak le jaye, to disk accesses kam ho sakte hain.

### Important Advantage

- Index size small
- Correct block quickly locate
- Memory requirement low

---

# 15. Multi-Level Index

Kabhi sparse index bhi itna large ho jata hai ke woh main memory mein fit nahi hota.

Example:

```text
100,000 records
10 records per block

≈ 10,000 data blocks
```

Agar har block ke liye ek index entry ho:

```text
≈ 10,000 index entries
```

Agar ek block mein 100 index entries fit hoti hain:

```text
10,000 / 100 = 100 index blocks
```

Ab 100 index blocks khud ek large structure ban gaye.

### Solution

**Index ke upar bhi index bana do.**

```text
Level 2 Index
      ↓
Level 1 Index
      ↓
Data Blocks
```

---

# 16. Real-Life Example of Multi-Level Index

Library:

```text
Library
   ↓
Floor
   ↓
Section
   ↓
Shelf
   ↓
Book
```

Tum directly poori library search nahi karti.

Har level search ko narrow karta hai.

Database mein:

```text
Outer Index
     ↓
Inner Index
     ↓
Data Block
     ↓
Record
```

### Main Idea

> **Index par index = Multi-Level Index**

Very large files ke liye additional levels bhi required ho sakte hain.

---

# 17. Binary Search in Index

Agar index blocks mein overflow nahi hai aur index ordered hai, to **binary search** efficiently use ki ja sakti hai.

Example:

```text
Index blocks = 100
```

Binary search mein approximately:

```text
log2(100) ≈ 7
```

block accesses mein correct block locate kiya ja sakta hai.

### Key Idea

Binary search sequential search se faster ho sakti hai jab ordered index structure available ho.

---

# 18. Index Update

Database mein index static nahi hota.

Jab bhi record:

- Insert hota hai
- Delete hota hai

to index ko bhi update karna padta hai.

---

# 19. Deletion in Index

Suppose data:

```text
10 Ali
20 Sara
30 Hina
```

Dense index:

```text
10 → Ali
20 → Sara
30 → Hina
```

Agar `20 Sara` delete ho jaye:

```text
10 → Ali
30 → Hina
```

Index bhi update karna padega.

---

# 20. Deletion in Sparse Index

Sparse index mein agar last record of a particular search key delete ho jaye, to suitable index entry remove/replace ki ja sakti hai.

Lecture ke basic rule ke according:

> Sparse index mein deleted key ki entry ko next appropriate search-key value se replace kiya ja sakta hai; agar new value ki already index entry ho to extra entry delete ki ja sakti hai.

---

# 21. Insertion in Dense Index

New record insert hua:

```text
105 → Ahmed
```

Dense index mein agar `105` new search-key value hai to:

```text
105 → New Record
```

ki index entry insert karni hogi.

---

# 22. Insertion in Sparse Index

Sparse index mein har insertion par index entry zaroori nahi hoti.

Usually change tab hota hai jab:

- New block create ho
- Block splitting/new block ki situation ho

Phir new block ka first search-key value index mein add kiya ja sakta hai.

---

# 23. Secondary Index

## Definition

Agar index ki search key file ke physical ordering ke same nahi hai, to usay **secondary index / non-clustering index** kehte hain.

### Example

Table physically `Emp_ID` ke order mein:

```text
101 Ali
102 Sara
103 Ali
104 Hina
```

Ab `Name` par index:

```text
Ali  → 101
Ali  → 103
Hina → 104
Sara → 102
```

Ye secondary index hai.

---

# 24. Why Secondary Index is Useful?

Suppose table mein employee ID primary key hai, lekin query frequently naam ke through hoti hai:

```sql
SELECT *
FROM Employee
WHERE Name = 'Ali';
```

Agar `Name` par secondary index hai, to database ko poori table scan karne ki zaroorat kam ho sakti hai.

### Main Benefit

> **Non-primary / alternate search key par fast queries.**

---

# 25. Why Secondary Index Must Often Be Dense?

Suppose:

```text
Name = Peterson
```

Aur Peterson ke records:

```text
Record 5
Record 20
Record 50
```

Physical table `Name` ke order mein stored nahi hai.

Isliye Peterson ke matching records file mein different locations par ho sakte hain.

Agar index sirf first record ka pointer rakhe:

```text
Peterson → Record 5
```

to Record 20 aur Record 50 ka location directly known nahi hoga.

Isliye secondary index ko all matching records ke pointers/locators maintain karne padte hain.

### Key Point ⭐

> **Secondary index on a non-candidate key generally needs pointers to all matching records.**

---

# 26. Bucket in Secondary Index

Multiple records same search-key value rakh sakte hain.

Example:

```text
Peterson → Bucket 2
```

Bucket:

```text
Bucket 2
   ↓
Record 5
Record 20
Record 50
```

Yahan ek extra level of indirection use hota hai.

### Simple Flow

```text
Secondary Index
      ↓
    Bucket
      ↓
Multiple Records
```

---

# 27. Candidate Key aur Secondary Index

Agar secondary search key **unique/candidate key** nahi hai, to same value ke multiple records ho sakte hain.

Example:

```text
Name = Ali
```

multiple employees ke liye same ho sakta hai.

Isliye:

```text
Ali → Record 10
Ali → Record 50
Ali → Record 70
```

multiple pointers required hain.

---

# 28. Secondary Index ka Drawback

Secondary indexes query performance improve karte hain, lekin database modification cost increase karte hain.

Suppose table mein:

```text
1 Primary/Clustered Index
3 Secondary Indexes
```

Agar ek record insert hota hai to database ko relevant indexes update karne pad sakte hain.

### Therefore

> More indexes = potentially faster reads + more maintenance on writes.

---

# 29. Composite Search Key

Agar ek index ki search key mein **multiple fields/columns** hon to usay:

- Composite Search Key
- Concatenated Key

kaha jata hai.

### Example

```text
(age, salary)
```

Yahan search key ke 2 fields hain:

```text
Age
Salary
```

---

# 30. Example of Composite Index

Employee table:

```text
Name    Age    Salary
Ali     20     10
Sara    20     20
Hina    25     30
Usman   30     50
```

Composite index:

```text
(age, salary)
```

Possible ordering:

```text
(20,10)
(20,20)
(25,30)
(30,50)
```

---

# 31. Composite Key Order Matters

Ye bohat important concept hai.

```text
(age, salary)
```

aur

```text
(salary, age)
```

same nahi hote.

Order change hone se index ki organization aur query usefulness change ho sakti hai.

### Example

```text
Index A = (age, salary)
Index B = (salary, age)
```

Ye dono different indexes hain.

---

# 32. Equality Query

Composite search key mein jab **har field ko exact value** di jaye, to equality query hoti hai.

Example:

```text
(age = 20 AND salary = 10)
```

Search key:

```text
(age, salary)
```

Dono values fixed hain.

### Rule

> **All composite-key fields fixed = Equality Query**

---

# 33. Range Query

Jab composite search key ke **all fields fixed na hon**, ya range condition use ho, to range query hoti hai.

Example 1:

```text
age = 20
```

Salary ki value specify nahi ki gayi.

Example 2:

```text
age < 30 AND salary > 40
```

Ye bhi range query hai.

### Rule

> **Not all fields fixed / range conditions = Range Query**

---

# 34. Equality vs Range Query

| Equality Query | Range Query |
|---|---|
| Every field has a constant value | One or more fields not fixed / range condition |
| Exact combination search | Broader set of records |
| Example: age=20 AND salary=10 | Example: age=20 |
| Composite key ke all fields bound | All fields bound nahi |

---

# 35. Important Example: Composite Index

Suppose:

```text
Index = (age, salary)
```

### Query 1

```sql
WHERE age = 20 AND salary = 10
```

This is:

```text
Equality Query
```

### Query 2

```sql
WHERE age = 20
```

This is:

```text
Range / Partial Query
```

because salary specify nahi ki gayi.

### Query 3

```sql
WHERE age < 30 AND salary > 40
```

This is:

```text
Range Query
```

---

# 36. Hashing vs Composite Search Key

Lecture ka important concept:

Hash-based file organization equality searches ke liye useful hota hai.

Agar composite hash key:

```text
(age, salary)
```

hai to desired bucket find karne ke liye normally dono values specify karni hoti hain.

Example:

```text
age = 20
salary = 10
```

exact values available hain.

Lekin:

```text
age = 20
```

mein salary missing hai, isliye hash structure direct exact bucket identify nahi kar pata in the same straightforward way.

### Important Idea

> **Hashing is mainly suited to equality searches; ordered indexes are more flexible for ordered/range searches.**

---

# 37. Why Indexes Improve Performance?

Main bottleneck aksar disk I/O hota hai.

Agar database ko 1,000 blocks scan karne parhein:

```text
Block 1
Block 2
Block 3
...
Block 1000
```

to time zyada lagega.

Index database ko correct area tak quickly guide karta hai.

```text
Index
  ↓
Relevant Block
  ↓
Required Record
```

### Main Idea

> **Fewer disk accesses = better performance**

---

# 38. But Too Many Indexes?

Indexes useful hain, lekin har column par index banana good idea nahi.

Because:

- Storage space increase hoti hai
- INSERT slow ho sakta hai
- DELETE slow ho sakta hai
- UPDATE slow ho sakta hai
- Har relevant index ko maintain karna padta hai

### Golden Rule

> **Indexes read performance improve karte hain, lekin write/maintenance cost add karte hain.**

---

# 39. Complete Comparison Table ⭐⭐⭐

| Feature | Clustered | Non-Clustered |
|---|---|---|
| Data order | Physically indexed order | Physically different order |
| Number | Usually one | Multiple |
| Main benefit | Fast ordered/range access | Fast alternate-key lookup |
| Data locator | Data structure closely represents rows | Pointers/locators to rows |

| Feature | Dense | Sparse |
|---|---|---|
| Entries | Every search-key value | Selected values |
| Size | Larger | Smaller |
| Search | Faster | Relatively slower |
| Maintenance | Higher | Lower |

| Feature | Primary | Secondary |
|---|---|---|
| Ordering | Same as file ordering | Different from file ordering |
| Typical use | Main ordering/search | Alternate search field |
| Duplicate values | Depends on key | Can have many matching records |
| Maintenance | Required | Required |

---

# 40. Real-World Example — Online Shopping Database

Suppose `Orders` table:

```text
Order_ID
Customer_ID
Order_Date
City
Amount
```

Possible indexes:

### Clustered Index

```text
Order_Date
```

Useful when query is:

```sql
SELECT *
FROM Orders
WHERE Order_Date BETWEEN '2026-07-01' AND '2026-07-31';
```

Because dates are physically ordered.

### Secondary Index

```text
Customer_ID
```

Useful for:

```sql
SELECT *
FROM Orders
WHERE Customer_ID = 5001;
```

### Composite Index

```text
(Customer_ID, Order_Date)
```

Useful when queries frequently filter by both:

```sql
WHERE Customer_ID = 5001
AND Order_Date = '2026-07-31';
```

---

# 41. Real-World Example — University Database

Students table:

```text
Student_ID
Name
Department
Semester
CGPA
```

Possible indexes:

### Primary/Clustered

```text
Student_ID
```

### Secondary

```text
Department
```

Query:

```sql
SELECT *
FROM Student
WHERE Department = 'CS';
```

### Composite

```text
(Department, Semester)
```

Query:

```sql
SELECT *
FROM Student
WHERE Department = 'CS'
AND Semester = 4;
```

---

# 42. Real-World Example — Hospital Database

Patients:

```text
Patient_ID
Name
Doctor_ID
Admission_Date
Disease
```

Possible indexes:

```text
Clustered → Patient_ID
Secondary → Doctor_ID
Secondary → Disease
Composite → (Doctor_ID, Admission_Date)
```

Why?

A hospital might frequently ask:

```sql
SELECT *
FROM Patients
WHERE Doctor_ID = 12;
```

or:

```sql
SELECT *
FROM Patients
WHERE Doctor_ID = 12
AND Admission_Date = '2026-07-30';
```

Indexes can make these searches much more efficient.

---

# 43. Exam-Focused Important Definitions

## Index

> A data structure used to speed up retrieval of records from a database file.

## Clustered Index

> An index that determines/reflects the physical ordering of data rows.

## Non-Clustered Index

> A separate index structure whose leaf entries point/locate the actual data rows.

## Dense Index

> An index containing an entry for every search-key value in the file.

## Sparse Index

> An index containing entries for only some search-key values.

## Primary Index

> An index whose search key corresponds to the sequential/physical ordering of the file.

## Secondary Index

> An index whose search key specifies an ordering different from the file's physical/sequential ordering.

## Composite Search Key

> A search key containing multiple fields, such as `(age, salary)`.

---

# 44. Important Short Questions

### Q1. What is the purpose of an index?

Index database records ko quickly locate karne aur query performance improve karne ke liye use hota hai.

### Q2. What is clustered index?

Clustered index data rows ki physical ordering determine/represent karta hai.

### Q3. How many clustered indexes can a table generally have?

Generally **one**.

### Q4. What is a dense index?

Har search-key value ke liye index entry hoti hai.

### Q5. What is a sparse index?

Sirf selected search-key values ke liye index entries hoti hain.

### Q6. Why is sparse index smaller?

Kyuki har record/search-key value ke liye entry nahi hoti.

### Q7. Why are secondary indexes generally dense?

Kyuki same search-key value ke multiple records file mein different locations par ho sakte hain; isliye all matching records ke locators needed hote hain.

### Q8. What is a composite search key?

A search key containing more than one field.

Example:

```text
(age, salary)
```

### Q9. What is a multi-level index?

Jab index bohat large ho aur us ke upar another index banaya jaye.

```text
Index
  ↓
Index
  ↓
Data
```

### Q10. What is the disadvantage of many indexes?

Storage aur INSERT/UPDATE/DELETE maintenance cost increase hoti hai.

---

# 45. Most Important Exam Differences

## Clustered vs Non-Clustered

```text
Clustered:
- Data physically ordered
- Usually one per table
- Good for range queries

Non-Clustered:
- Data physically ordered according to this index nahi
- Multiple possible
- Contains locators/pointers
```

## Dense vs Sparse

```text
Dense:
- Entry for every search-key value
- Faster
- More space

Sparse:
- Entry for selected values
- Less space
- Relatively slower
```

## Primary vs Secondary

```text
Primary:
- Same ordering as file
- Main/physical ordering

Secondary:
- Different ordering
- Alternate search field
- Often needs pointers to all matching records
```

## Equality vs Range

```text
Equality:
age = 20 AND salary = 10

Range:
age = 20
age < 30
age < 30 AND salary > 40
```

---

# 46. Super Easy Memory Tricks

### INDEX

> **Index = Shortcut for searching**

### CLUSTERED

> **Clustered = Data is clustered/physically ordered**

### NON-CLUSTERED

> **Non-clustered = Index separate, pointer to data**

### DENSE

> **Dense = Every value**

### SPARSE

> **Sparse = Selected values**

### PRIMARY

> **Primary = File ki main/sequential ordering**

### SECONDARY

> **Secondary = Another/alternate search field**

### MULTI-LEVEL

> **Index of an index**

### COMPOSITE

> **Multiple columns in one search key**

---

# 47. Final 5-Minute Revision

Agar exam se just pehle time bohat kam ho to ye section zaroor parho:

```text
1. Index records ko fast search karne ka shortcut hai.

2. Clustered index data ko indexed key ke order mein physically organize karta hai.

3. Usually one table has one clustered index.

4. Non-clustered index separate structure hota hai jo actual rows ko pointers/locators se identify karta hai.

5. Dense index mein har search-key value ki entry hoti hai.

6. Sparse index mein sirf selected entries hoti hain, isliye space kam lagta hai.

7. Primary index file ki sequential/physical ordering wali key par hota hai.

8. Secondary index alternate/non-primary search key par hota hai aur duplicate values ke case mein multiple records ke locators chahiye hote hain.

9. Multi-level indexing mein index ke upar index banaya jata hai.

10. Composite search key mein multiple fields hoti hain:
   (age, salary)

11. Equality query:
   age = 20 AND salary = 10

12. Range query:
   age = 20
   or
   age < 30 AND salary > 40

13. More indexes → faster reads but more storage and update/maintenance cost.

14. Index update must happen after relevant INSERT and DELETE operations.
```

---

# 48. One-Page Concept Map

```text
INDEX
│
├── Ordered Index
│   │
│   ├── Primary / Clustering
│   │
│   └── Secondary / Non-Clustering
│
├── Density
│   │
│   ├── Dense
│   └── Sparse
│
├── Multi-Level Index
│   │
│   └── Index → Index → Data
│
└── Composite Search Key
    │
    ├── Equality Query
    │   └── All fields fixed
    │
    └── Range Query
        └── Not all fields fixed / range conditions
```

---

# 49. Final Summary

Lecture 38 ka central idea ye hai ke **database indexes searching ko fast banate hain**.

Sabse important concepts:

```text
INDEX
   ↓
Fast Retrieval

CLUSTERED
   ↓
Physical Data Order

NON-CLUSTERED
   ↓
Separate Index + Row Locator

DENSE
   ↓
Every Search-Key Value

SPARSE
   ↓
Selected Search-Key Values

PRIMARY
   ↓
File ki Ordering wali Key

SECONDARY
   ↓
Alternate Search Key

MULTI-LEVEL
   ↓
Index of Index

COMPOSITE
   ↓
Multiple Fields
```

## Golden Exam Line

> **Clustered = physical order, Dense = every value, Sparse = some values, Secondary = alternate search key, Multi-level = index of index, Composite = multiple fields.**

---

# Quick MCQ Facts

1. **Which index determines physical data order?**  
   → Clustered Index

2. **Which index normally has one per table?**  
   → Clustered Index

3. **Which index has an entry for every search-key value?**  
   → Dense Index

4. **Which index requires less storage?**  
   → Sparse Index

5. **Which index is used for alternate search keys?**  
   → Secondary Index

6. **Which index may contain pointers to multiple matching records?**  
   → Secondary Index

7. **What is an index on `(age, salary)` called?**  
   → Composite Index/Search Key

8. **`age = 20 AND salary = 10` is what type of query?**  
   → Equality Query

9. **`age = 20` using `(age, salary)` is what type?**  
   → Range/Partial Query

10. **Index on index is called?**  
    → Multi-Level Index

---

# End of Lecture 38

## Most Important Formula in Your Mind

```text
Fast Search
   ↓
INDEX

Physical Order
   ↓
CLUSTERED

Every Value
   ↓
DENSE

Some Values
   ↓
SPARSE

Alternate Key
   ↓
SECONDARY

Multiple Levels
   ↓
MULTI-LEVEL

Multiple Fields
   ↓
COMPOSITE
```
