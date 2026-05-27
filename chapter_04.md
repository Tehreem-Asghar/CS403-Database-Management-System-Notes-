# 📘 Database Management System (CS403) — Lecture No. 04 Detailed Notes

# Topics Covered

- Internal Schema / Physical View
- Inter Schema Mapping
- Data Independence
- Logical Data Independence
- Physical Data Independence
- Functions of DBMS
- DBMS Environments
- Real Life Examples

---

# 🔷 1. Internal Schema / Physical View

Internal Schema database ka wo level hota hai jo data ko storage devices (hard disk, SSD, etc.) par physically store karta hai.

Ye level decide karta hai:

- Data disk par kaise save hoga
- Data kis format me hoga
- Storage kaise optimize hogi
- Security kaise maintain hogi

---

# 🔹 Important Point

User directly physical level ko nahi dekhta.

Sirf DBMS hi internal level ko samajhta hai.

---

# 🔷 Binary Storage

Computer har type ka data binary format me store karta hai.

Chahe:

- Text ho
- Image ho
- Audio ho
- Video ho

Sab kuch `0` aur `1` ki form me store hota hai.

---

# ✅ Real Life Example

Aap mobile me photo save karte ho.

Aapko image nazar aati hai, lekin internally wo binary data hoti hai.

Example:

```txt
101010101011001010101
```

---

# 🔷 DBMS Additional Information Store Karta Hai

DBMS data ke sath kuch extra information bhi store karta hai.

Jaise:

- Indexes
- Record Headers
- Block Headers

Ye information fast searching aur retrieval ke liye use hoti hai.

---

# ✅ Real Life Example

Google Drive me file search karna fast hota hai kyunki indexing use hoti hai.

---

# 🔷 Data Compression

DBMS storage bachane ke liye data compress bhi karta hai.

Purpose:

- Kam storage use ho
- Performance slow na ho

---

# ✅ Real Life Example

ZIP file compression.

---

# 🔷 Data Security

Database ko secure rakhne ke liye encryption algorithms use kiye jate hain.

---

# ✅ Real Life Example

ATM database me user PIN encrypted form me store hota hai.

---

# 🔷 Internal Level vs Physical Level

| Internal Level | Physical Level |
|---|---|
| Record format me data | Binary format me data |
| DBMS manage karta hai | Operating System manage karta hai |
| Schema rules apply hote hain | Sirf storage hoti hai |

---

# 🔷 Record Header aur Block Header

## Record Header (RH)

Har record ke start me extra information.

## Block Header (BH)

Records ke group ke start me extra information.

---

# ✅ Real Life Example

Library books:

- Book = Record
- Shelf = Block

---

# 🔷 Block-wise Storage

Disk par data record-wise nahi balki block-wise store hota hai.

Isse:

- Disk operations kam hote hain
- Speed improve hoti hai

---

# 🔷 2. Inter Schema Mapping

Mapping ka matlab hai:

Ek level ke data ko doosre level ke format se relate karna.

---

# 🔷 Types of Mapping

## 1. External / Conceptual Mapping

External view aur conceptual level ko connect karta hai.

## 2. Conceptual / Internal Mapping

Conceptual aur internal levels ko connect karta hai.

---

# ✅ Real Life Example

Database me:

```txt
Date of Birth = 2000
```

User ko show ho:

```txt
Age = 25
```

Ye conversion mapping perform karti hai.

---

# 🔷 3. Data Independence

Data Independence database ki bohat important feature hai.

Ye allow karti hai ke database me changes hon lekin applications affect na hon.

---

# ✅ Real Life Example

Website ka database upgrade ho jaye lekin website normal chalti rahe.

---

# 🔷 Types of Data Independence

1. Logical Data Independence
2. Physical Data Independence

---

# 🔷 4. Logical Data Independence

Conceptual level me changes external views ko affect nahi karte.

---

# ✅ Allowed Changes

- New field add karna
- New file add karna
- Data type change karna

---

# ❌ Dangerous Change

Attribute delete karna.

Kyuki applications us attribute ko use kar rahi hoti hain.

---

# ✅ Real Life Example

Student table me:

```txt
Phone Number
```

field add karna safe hai.

Lekin:

```txt
Student ID
```

delete karna dangerous hai.

---

# 🔷 5. Physical Data Independence

Internal level me changes conceptual level ko affect nahi karte.

---

# ✅ Allowed Changes

- Storage media change karna
- File organization change karna
- Indexing technique change karna

---

# ✅ Real Life Example

Database HDD se SSD par move karna.

Applications phir bhi same tarah work karti hain.

---

# 🔷 6. Functions of DBMS

## Major Functions

- Data Processing
- Catalog Management
- Transaction Support
- Concurrency Control
- Recovery Services
- Authorization
- Communication Support
- Integrity Services

---

# 🔷 6.1 Data Processing

DBMS data ko:

- Create karta hai
- Store karta hai
- Arrange karta hai
- Retrieve karta hai

---

# ✅ Real Life Example

Bank ATM transaction processing.

---

# 🔷 6.2 User Accessible Catalog

Catalog database ki information store karta hai.

Jaise:

- Tables
- Users
- Permissions
- Schema

---

# ✅ Real Life Example

School register system.

---

# 🔷 6.3 Transaction Support

Transaction database par operation hota hai.

---

# ✅ Real Life Example

ATM se paise withdraw karna.

Steps:

1. Balance check
2. Amount deduct
3. Cash dispense

Ye sab ek transaction hai.

---

# 🔷 6.4 Concurrency Support

Multiple users ko same time database access karne ki facility.

---

# ✅ Real Life Example

Online shopping website.

Thousands users ek sath products buy karte hain.

---

# 🔷 6.5 Recovery Services

Agar database corrupt ho jaye to DBMS usko recover karta hai.

---

# ✅ Real Life Example

Electricity chali jaye during transaction.

DBMS incomplete transaction rollback kar deta hai.

---

# 🔷 6.6 Authorization Services

DBMS decide karta hai:

- Kaun access karega
- Kya access karega

---

# ✅ Real Life Example

Teacher marks edit kar sakta hai.

Student sirf marks dekh sakta hai.

---

# 🔷 6.7 Support for Data Communication

Different locations ke users ko database connect karta hai.

---

# ✅ Real Life Example

Bank branches different cities me connected hoti hain.

---

# 🔷 6.8 Integrity Services

Database me sirf correct data allow hota hai.

---

# ✅ Real Life Example

Age field me:

```txt
-5
```

allow nahi hoga.

---

# 🔷 7. DBMS Environments

## Types

1. Single User
2. Multi User

---

# 🔷 7.1 Single User Environment

Ek waqt me sirf ek user database use karta hai.

---

# ✅ Real Life Example

MS Access desktop database.

---

# 🔷 7.2 Multi User Environment

Multiple users simultaneously database use karte hain.

---

# 🔷 Types of Multi User Systems

- Teleprocessing
- File Server
- Client-Server

---

# 🔷 Teleprocessing

Sab requests central computer process karta hai.

---

# ✅ Real Life Example

Old banking systems.

---

# 🔷 File Server

Database server par hota hai.

Complete file client ko bheji jati hai.

---

# ❌ Problem

Network traffic zyada hota hai.

---

# ✅ Real Life Example

Old office shared file systems.

---

# 🔷 Client-Server Architecture

Modern DBMS architecture.

Client request bhejta hai.

Server processing karta hai.

Result wapas bhejta hai.

---

# ✅ Real Life Example

Facebook
Instagram
Online Banking Systems

---

# 🔷 Three Level Database Architecture Summary

| Level | Description |
|---|---|
| External Level | User View |
| Conceptual Level | Logical Structure |
| Internal Level | Storage Structure |
| Physical Level | Binary Storage |

---

# 🔷 Advantages of Three Level Architecture

- Data Independence
- Better Security
- Better Performance
- Easy Maintenance
- Multiple User Views

---

# 🔷 Important Short Definitions

| Term | Definition |
|---|---|
| Schema | Database structure |
| Mapping | Connection between levels |
| Data Independence | Changes without affecting applications |
| Transaction | Database operation |
| Concurrency | Multiple users same time |
| Integrity | Correctness of data |
| Authorization | Permission control |

---

# 🔷 Final Conclusion

Three Level Architecture database systems ko:

- Flexible
- Secure
- Efficient
- Maintainable

banati hai.

DBMS data ko manage karta hai aur users ko secure aur fast access provide karta hai.

---
