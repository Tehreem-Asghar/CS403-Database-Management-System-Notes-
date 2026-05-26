# Database Management System (CS403)  
# Lecture No. 01 Detailed Notes

---

# 📘 Introduction to Databases

Database Management System (DBMS) ek aisa system hai jo data ko:
- store karta hai
- manage karta hai
- organize karta hai
- retrieve karta hai

Database ka main purpose data ko efficiently handle karna hota hai.

---

# 📌 Course Introduction

Is course mein hum databases ke:
- theoretical concepts
- practical implementation
- database design
- SQL
- DBMS tools

study karenge.

---

# 📌 Areas Covered in This Course

## 1. Database Design and Application Development

Hum seekhenge:
- Real-world system ko database mein kaise convert karte hain
- Tables kaise design hoti hain
- Relationships kaise banti hain

### ✅ Real Life Example
School management system:
- Students table
- Teachers table
- Courses table

Sab tables mil kar ek database system banayengi.

---

## 2. Concurrency and Robustness

Concurrency ka matlab:
Multiple users ek hi waqt mein database access kar saken.

### ✅ Example
Bank system:
- Ek user paise withdraw kar raha hai
- Dusra user balance check kar raha hai

DBMS dono operations safely handle karta hai.

---

## 3. Efficiency and Scalability

Database large amount of data ko efficiently handle karta hai.

### ✅ Example
Facebook jaisi applications:
- Millions of users
- Billions of posts

DBMS efficiently data manage karta hai.

---

# 📘 Study of Database Tools

Database ko practically use karne ke liye tools ki zaroorat hoti hai.

## 📌 SQL

SQL ka full form:
Structured Query Language

SQL use hoti hai:
- data insert karne
- update karne
- delete karne
- retrieve karne

### ✅ Example
```sql
SELECT * FROM Students;
```

Ye query Students table ka sara data show karegi.

---

## 📌 DBMS

DBMS ek software hota hai jo database ko manage karta hai.

### ✅ Examples of DBMS
- MySQL
- Oracle
- SQLite
- PostgreSQL
- Microsoft SQL Server

Example:
:contentReference[oaicite:0]{index=0}

---

# 📘 Database Definitions

Different books mein databases ki different definitions di gayi hain.

---

## 📌 Definition 1

Database logically related data ka shared collection hota hai jo organization ke multiple users ki information needs ko fulfill karta hai.

### ✅ Important Terms

### 🔹 Shared Collection
Data multiple users use karte hain.

### 🔹 Logically Related
Data ka apas mein relation hota hai.

### ✅ Example
University database:
- Students
- Courses
- Teachers

Sab data ek dusre se related hai.

---

## 📌 Definition 2

Database organized data ka collection hota hai jo computer mein store hota hai aur easily search kiya ja sakta hai.

### ✅ Example
Google search database.

---

## 📌 Definition 3

Database metadata bhi store karta hai.

### 🔹 Metadata
Data about data.

### ✅ Example
Student age integer type hai.

Ye metadata hai.

---

# 📘 Difference Between Database and DBMS

| Database | DBMS |
|---|---|
| Data ka collection | Data manage karne ka software |
| Information store karta hai | Database ko control karta hai |
| Passive | Active |

---

## ✅ Example

### Database
Students ka data:
- name
- roll number
- age

### DBMS
Software jo:
- data insert karta hai
- delete karta hai
- update karta hai

Example:
:contentReference[oaicite:1]{index=1}

---

# 📘 Examples of Data

| Thing | Stored Data |
|---|---|
| Cricket Player | Name, country, runs |
| Movie | Name, director |
| Vehicle | Registration number, owner |
| Food | Ingredients, taste |

---

# 📘 Perspective Changes Data

Database mein kya data store hoga ye user ke perspective par depend karta hai.

---

## ✅ Example: Karahi Gosht

### 👨‍🍳 Cook Perspective
- salt quantity
- cooking time
- ingredients

### 👨 Customer Perspective
- price
- chicken ya mutton
- spicy ya normal

---

# 📘 Importance of Databases

Databases modern life ka important part hain.

---

# 📌 Types of Applications

## 1. Scientific Applications

Ye applications heavy calculations karti hain.

### ✅ Examples
- Space research
- Nuclear systems
- Medical systems

---

## 2. Commercial Applications

Ye applications mainly:
- data store
- retrieve
- process

karti hain.

### ✅ Examples
- Banks
- Shopping systems
- Billing systems

---

# 📘 Traditional File Processing System

Database se pehle organizations file processing systems use karti thi.

---

# 📌 Manual File System

Data paper files mein store hota tha.

### ❌ Problems
- Slow
- Time consuming
- Difficult management

---

# 📌 Computerized File System

Manual work ko computer par shift kiya gaya.

Processing fast hui lekin naye problems bhi aaye.

---

# 📘 Problems in Traditional File Processing System

---

# 📌 1. Program-Data Dependence

Program aur data ek dusre par depend karte hain.

Agar data structure change ho:
- program bhi change hoga

---

## ✅ Example

Bill file mein customer address add karna.

Affected:
- bill print program
- bill calculate program

Chahe calculate program ko address ki zaroorat na ho.

---

# 📌 2. Data Redundancy

Same data multiple places par store hota hai.

---

## ✅ Example

Student name:
- library file
- examination file
- registration file

Har jagah separately stored.

---

# 📌 3. Data Inconsistency

Different systems mein same data different ho jata hai.

---

## ✅ Example

Library system:
Ahmed

Examination system:
Ahmad

Ye inconsistency hai.

---

# 📘 Database System Environment

Database environment mein:
- data central place par store hota hai
- DBMS sab manage karta hai

---

# 📌 Educational Institution Example

Applications:
- Library System
- Examination System
- Registration System

Sab ek hi database use karte hain.

---

# 📘 Advantages of Databases

---

# 📌 1. Data Sharing

Same data sab applications share karti hain.

### ✅ Example
Student data:
- name
- roll number
- address

Ek hi jagah store hota hai.

---

# 📌 2. Data Independence

Programs aur data independent hote hain.

### ✅ Benefit
Data structure change ho to har program change nahi karna padta.

---

# 📌 3. Controlled Redundancy

Duplicate data ko control kiya jata hai.

### ✅ Benefit
Storage waste nahi hoti.

---

# 📌 4. Better Data Integrity

Database valid data ensure karta hai.

---

## ✅ Example

Age field mein:
```text
Age = Twenty
```

Invalid hai.

Correct:
```text
Age = 20
```

---

# 📘 Why Data Integrity Important?

Agar data wrong hoga:
- reports wrong hongi
- decisions wrong honge

---

## ✅ Real Life Example

Bank database mein balance wrong ho gaya.

Result:
- wrong transactions
- financial loss

---

# 📘 Database System

Database + DBMS = Database System

---

# 📘 Real Life Examples of Database Systems

| System | Stored Data |
|---|---|
| Railway Reservation | Passenger records |
| Hospital System | Patient records |
| School System | Student records |
| Banking System | Account details |

---

# 📘 Exercises

## Exercise 1
Apne around 5 cheezon ka data sochiye jo database mein store ho sakta hai.

---

## Exercise 2
Railway Reservation System mein possible changes ki list banayein.

### ✅ Example Changes
- Online booking
- Seat selection
- Mobile payment
- Passenger CNIC addition

---

# 📘 Important Short Notes

| Topic | Key Point |
|---|---|
| Database | Organized data collection |
| DBMS | Database management software |
| SQL | Database manipulation language |
| Redundancy | Duplicate data |
| Integrity | Correct data |
| Concurrency | Multiple users access |
| Data Sharing | Same data shared |

---

# 📘 Conclusion

Database systems modern organizations ke liye bohat important hain.

Ye:
- data efficiently manage karte hain
- redundancy reduce karte hain
- integrity maintain karte hain
- sharing allow karte hain

Traditional file systems ki problems ko databases solve karte hain.

---
