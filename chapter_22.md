# CS403 – Database Management System
# Lecture 22 – Physical Database Design (Complete Notes)
---

# 📚 Lecture Overview

Is lecture mein hum ye topics seekhenge:

- Physical Database Design
- Data Volume Analysis
- Data Usage Analysis
- Designing Fields
- Choosing Data Types
- Coding Techniques
- Coding Example
- Default Values
- Range Control
- NULL Value Control
- Referential Integrity

---

# 1. Physical Database Design Kya Hota Hai?

Database banane ke do major stages hoti hain.

## Stage 1 – Logical Design

Is stage mein sirf planning hoti hai.

Hum decide karte hain:

- Kitni tables hongi
- Kis table mein kya data hoga
- Primary Key kya hogi
- Foreign Key kya hogi
- Relationships kya hongi

Example

```
Student
--------
StudentID
Name
Age
DepartmentID
```

Yeh sirf planning hai.

Abhi database create nahi hua.

---

## Stage 2 – Physical Design

Ab hum is planning ko actual DBMS (MySQL, Oracle, SQL Server) mein implement karte hain.

Yahan decide hota hai:

- Data kis data type mein store hoga
- Kitni storage lagegi
- Hard disk par data kaise save hoga
- Index banega ya nahi
- Queries ko fast kaise banana hai

Yahi Physical Database Design kehlata hai.

---

# Simple Definition

> Physical Database Design ka matlab hai logical design ko actual database mein efficiently implement karna taake database fast, secure aur kam storage use kare.

---

# Real Life Example

Socho aap ghar banwa rahe ho.

## Logical Design

Architect map banata hai.

- Bedroom kidhar hoga
- Kitchen kidhar hogi
- Washroom kidhar hoga

Abhi ghar bana nahi.

---

## Physical Design

Ab mason aata hai.

- Cement lagata hai
- Eent lagata hai
- Darwaze install karta hai

Yani actual construction hoti hai.

Database mein bhi bilkul isi tarah hota hai.

---

# 2. Physical Design Se Pehle Kya Ready Hona Chahiye?

Physical Design tabhi shuru hota hai jab kuch important kaam complete ho chuke hon.

| Requirement | Roman Urdu Meaning |
|-------------|--------------------|
| Normalization | Duplicate data remove ho chuka ho |
| Volume Estimate | Kitna data aayega iska andaza ho |
| Attribute Definition | Har field ka meaning clear ho |
| Data Usage | Data kitni baar use hoga |
| Response Time | Kitni speed chahiye |
| Security | Data kitna secure hona chahiye |

---

# Example

Hospital Database

Doctor Records = 200

Patients = 1000

Medicines = 500

Appointments = 10000

Agar pehle hi estimate ho to database future mein slow nahi hota.

---

# 3. Data Volume Analysis

## Volume ka Matlab

Database kitna bada hoga.

Yani total records kitne honge.

---

## Example 1

School

Students = 300

Storage kam lagegi.

---

## Example 2

University

Students = 80,000

Storage zyada lagegi.

---

## Example 3

Facebook

Users = Billions

Storage bohot zyada.

---

# Volume Estimate Kyun Zaroori Hai?

Agar database chhota hai

To simple design kaafi hai.

Agar database bohot bada hai

To:

- Index banana padega
- Compression karni padegi
- Fast storage use hogi

---

# 4. Data Usage Analysis

Volume sirf size batata hai.

Usage batata hai data kitni baar use hota hai.

---

## Example

Student Table

| StudentID | Name | Blood Group |
|------------|------|-------------|
| S101 | Ali | B+ |

Roz search hota hai

✅ StudentID

Kabhi kabhi search hota hai

❌ Blood Group

To StudentID ko optimize kiya jayega.

---

# Example

ATM Machine

Har second Account Number search hota hai.

Date of Birth bohot kam search hoti hai.

To Account Number par index banega.

---

# 5. Physical Database Design Steps

Lecture mein diye gaye important steps.

---

## Step 1

Correct Attributes Select Karna

Har field useful honi chahiye.

Example

```
StudentID
Name
Email
Phone
```

---

## Step 2

Correct Data Type Select Karna

Galat

```
Age = VARCHAR
```

Sahi

```
Age = INTEGER
```

---

## Step 3

Fields ko Logical Order mein Rakhna

Wrong

```
Age
Name
StudentID
```

Correct

```
StudentID
Name
Age
Department
```

Readable bhi hai.

---

## Step 4

Hard Disk Storage Decide Karna

Data disk mein kaise save hoga.

Database decide karta hai

- Records kis order mein save hon
- Kahan save hon
- Kitni speed se read hon

---

## Step 5

Indexes Banana

Jo fields roz search hoti hain un par index banta hai.

Example

Phone Contacts

```
A
B
C
D
```

Ye bhi ek tarah ka index hai.

---

## Step 6

Queries Optimize Karna

Example

```sql
SELECT *
FROM Student
WHERE StudentID='S102';
```

Agar StudentID indexed hai

To query milliseconds mein chalti hai.

---

# 6. Field Kya Hota Hai?

Field database ka sabse chhota part hota hai.

Example

| StudentID | Name | Age |
|------------|------|-----|
| S101 | Ali | 20 |

Yahan

StudentID = Field

Name = Field

Age = Field

---

# 7. Data Type Kya Hota Hai?

Data Type decide karta hai

Field mein kis type ki value store hogi.

---

## Example

Age

```
18
20
25
```

Sirf numbers.

---

Name

```
Ali
Ahmed
Sara
```

Sirf text.

---

Date

```
30-07-2026
```

Sirf date.

---

# 8. Data Types Use Karne Ke Objectives

Lecture ke mutabiq 4 objectives hain.

---

## Objective 1

Storage Bachana

Galat

```
Name VARCHAR(500)
```

Agar maximum 30 letters hain to

Correct

```
Name VARCHAR(30)
```

Storage bach gayi.

---

## Objective 2

Har Valid Value Store Ho

Age

```
18
20
40
```

Sab save hon.

---

## Objective 3

Data Integrity Improve Karna

Age mein

```
Twenty
```

Store nahi hona chahiye.

Sirf number aaye.

---

## Objective 4

Data Manipulation Easy Ho

Data Type ki wajah se

- Searching
- Sorting
- Calculations

Sab easy hoti hain.

---

# 9. Common Data Types

| Data Type | Use | Example |
|------------|-----|----------|
| CHAR | Fixed Length Text | Gender, Code |
| VARCHAR2 | Variable Text | Name |
| NUMBER | Numbers | Age |
| DATE | Date | DOB |
| LONG | Long Text | Description |
| RAW | Binary Data | System Data |
| LONG RAW | Large Binary Data | Machine Data |
| BLOB | Images, PDF, Videos | Student Photo |

---

# 10. CHAR Data Type

Fixed Length Data

Example

```
Gender

M
F
```

Ya

```
Country Code

PK
US
IN
```

Length same rehti hai.

---

# 11. VARCHAR2

Variable Length

Example

```
Ali
Ahmed
Muhammad Bilal
```

Har name ki length different hai.

Isliye VARCHAR use hota hai.

---

# 12. NUMBER

Sirf Numbers

Example

```
Age

18

Salary

60000

Marks

95
```

---

# 13. DATE

Dates store karta hai.

Example

```
30-07-2026
```

Ya

```
01-01-2025
```

---

# 14. BLOB

BLOB ka matlab

Binary Large Object

Isme store hote hain

- Images
- Videos
- PDFs
- Audio
- Documents

Example

Student ki photo database mein.

---

# 15. Coding Technique

Kabhi ek hi value hazaron baar repeat hoti hai.

Example

| Student | Hobby |
|----------|--------|
| Ali | Reading |
| Ahmed | Reading |
| Sara | Reading |
| Bilal | Reading |

Har row mein Reading likhne se storage waste hoti hai.

---

# Solution

Reading ki jagah

Sirf

```
R
```

Store karo.

---

# Hobby Table

| Code | Hobby |
|------|--------|
| R | Reading |
| G | Gardening |
| M | Movies |

---

# Student Table

| Student | Hobby Code |
|----------|------------|
| Ali | R |
| Ahmed | G |
| Sara | M |
| Bilal | R |

---

# Is Technique Ke Fayde

✅ Storage bachti hai

✅ Database fast hota hai

✅ Data duplicate nahi hota

✅ Updates easy hoti hain

---

# Real Life Example

Country

Wrong

```
Pakistan
Pakistan
Pakistan
Pakistan
```

Correct

```
PK
```

Country Table

| Code | Country |
|------|----------|
| PK | Pakistan |
| IN | India |
| US | United States |

---

# 16. Default Value

Default Value wo hoti hai

Jo automatically save ho jati hai agar user koi value enter na kare.

---

Example

Country

Default

```
Pakistan
```

Agar user blank chhod de

To automatically

```
Pakistan
```

Save ho jayega.

---

Another Example

Status

Default

```
Active
```

Har naye employee ka status automatically Active hoga.

---

# Default Value Ke Benefits

- User ki mehnat kam hoti hai
- Wrong values kam aati hain
- Empty fields nahi rehti

---

# 17. Range Control

Range Control ka matlab

Value sirf ek limit ke andar honi chahiye.

---

Example

Age

Allowed

```
1–100
```

Agar user

```
250
```

Likhe

Database error dega.

---

Another Example

Marks

Allowed

```
0–100
```

User

```
150
```

Likhe

Reject ho jayega.

---

# Range Control Ke Benefits

✅ Invalid data save nahi hota

✅ Data accurate rehta hai

---

# 18. NULL Value Control

NULL ka matlab

Koi value available hi nahi.

NULL

≠ Zero

≠ Blank Space

---

Example

Phone Number

```
NULL
```

Matlab phone number diya hi nahi.

---

Example

Salary

```
0
```

Matlab salary zero hai.

Ye NULL nahi.

---

Example

Name

```
" "
```

Ye blank space hai.

Ye bhi NULL nahi.

---

# NULL Control

Kuch fields compulsory hoti hain.

Example

StudentID

NULL allowed?

❌ Nahi

Name

NULL allowed?

❌ Nahi

Phone Number

NULL allowed?

✅ Ho sakta hai

---

# 19. Referential Integrity

Ye database ka bohot important concept hai.

Iska matlab

Foreign Key ki value hamesha Parent Table mein honi chahiye.

---

## Department Table

| DeptID | Department |
|--------|------------|
| D01 | CS |
| D02 | IT |
| D03 | SE |

---

## Student Table

| Student | DeptID |
|----------|--------|
| Ali | D01 |
| Ahmed | D02 |

Ye bilkul sahi hai.

---

Agar koi likhe

| Student | DeptID |
|----------|--------|
| Sara | D99 |

Database error dega.

Kyun?

Kyun ke D99 Department Table mein exist hi nahi karta.

Isi ko Referential Integrity kehte hain.

---

# Real Life Example

Socho

Classroom mein sirf

Roll Numbers

```
101
102
103
```

Maujood hain.

Agar koi attendance mein

```
999
```

Likhe

Teacher foran kahega

"Ye student hamari class mein hai hi nahi."

Database bhi bilkul isi tarah check karta hai.

---

# 🎯 Interview / Exam Tips

### Physical Database Design

Logical design ko actual database mein implement karna.

---

### Data Volume Analysis

Database ka size estimate karna.

---

### Data Usage Analysis

Kaunsa data kitni baar use hota hai.

---

### Field

Table ka sabse chhota data item.

---

### Data Type

Field kis type ka data store karegi.

---

### Coding Technique

Badi values ki jagah chhote codes use karna.

---

### Default Value

Automatic value jo user ke bina input ke save ho jaye.

---

### Range Control

Sirf allowed range ki values accept karna.

---

### NULL

Missing value.

Zero ya blank nahi.

---

### Referential Integrity

Foreign Key ki value Parent Table mein zaroor exist karni chahiye.

---

# 📌 Complete Lecture Summary

- Physical Database Design database banane ka practical stage hai.
- Is se pehle Normalization, Volume Estimate aur Attribute Definition complete honi chahiye.
- Data Volume Analysis database ke future size ka estimate deta hai.
- Data Usage Analysis batata hai ke kaunsa data sabse zyada access hota hai.
- Har field ke liye sahi Data Type select karna performance aur storage dono ke liye important hai.
- CHAR fixed length ke liye aur VARCHAR variable length text ke liye use hota hai.
- NUMBER numeric values, DATE dates aur BLOB images/files ke liye use hota hai.
- Coding Technique (jaise Reading = R) storage bachati aur performance improve karti hai.
- Default Values automatically fill hoti hain jab user value enter na kare.
- Range Control invalid values ko reject karta hai.
- NULL ka matlab value available nahi hai, aur ye 0 ya blank space se mukhtalif hota hai.
- Referential Integrity ensure karti hai ke Foreign Key hamesha Parent Table ki valid value ko refer kare.
