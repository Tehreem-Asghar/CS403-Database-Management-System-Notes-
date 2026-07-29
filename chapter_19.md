# 📘 CS403 – Database Management Systems
# Lecture 19 Notes (Functional Dependency, Inference Rules & Normalization)
---

# 📖 Introduction

Pichli lecture mein hum ne **Joins** padhe thay.

Join ka kaam tha:

- Do ya zyada tables ko combine karna.

Ab is lecture mein hum aik naya concept parhenge jiska naam hai

# Normalization

Normalization Database Design ka sab se important topic hai.

Agar Normalization samajh aa gayi to:

✅ Database achi design hogi

✅ Duplicate data nahi hoga

✅ Database fast chalega

✅ Errors kam hongi

Isi wajah se interview aur exams dono mein is topic se questions zaroor aate hain.

---

# Real Life Example

Socho aik school hai.

Teacher ne students ki information is tarah save ki.

|Student ID|Name|Department|Department HOD|
|----------|------|-----------|---------------|
|101|Ali|CS|Ahmed|
|102|Sara|CS|Ahmed|
|103|Usman|CS|Ahmed|

Yahan dekho

Department ka naam har row mein repeat ho raha hai.

HOD ka naam bhi repeat ho raha hai.

Agar HOD change ho gaya to teenon rows update karni hongi.

Agar ek row update karna bhool gaye to database galat ho jayega.

Isi problem ko solve karne ke liye **Normalization** use hoti hai.

---

# Functional Dependency (FD)

Normalization ki foundation hai

# Functional Dependency

Sab se pehle FD samajhna zaroori hai.

---

# Functional Dependency ki Simple Definition

Agar kisi ek attribute ki value jaan kar hum kisi doosre attribute ki value hamesha bata saken,

to usay kehte hain

**Functional Dependency**

Notation:

```
A → B
```

Read:

```
A determines B
```

ya

```
B is functionally dependent on A
```

---

# Sab se Easy Example

Suppose

|Roll No|Student Name|
|---------|-------------|
|101|Ali|
|102|Sara|
|103|Usman|

Agar koi kahe

```
Roll No = 102
```

To foran hum bata sakte hain

```
Student Name = Sara
```

Isliye

```
RollNo → StudentName
```

Yani

Roll Number Student Name ko determine karta hai.

---

# Ek aur Example

|CNIC|Name|Gender|
|------|------|-------|
|35201|Ali|Male|

CNIC unique hota hai.

CNIC dekh kar hum Name aur Gender dono bata sakte hain.

```
CNIC → Name

CNIC → Gender
```

---

# Important Point

Functional Dependency ka matlab

❌ Formula nahi hota.

❌ Calculation nahi hoti.

Sirf itna matlab hota hai

Ek value se doosri value uniquely mil jaye.

---

# Determinant aur Dependent

FD mein

```
StudentID → StudentName
```

Left side

```
StudentID
```

ko kehte hain

**Determinant**

Right side

```
StudentName
```

ko kehte hain

**Dependent**

Yaad rakho

```
Left Side = Determinant

Right Side = Dependent
```

---

# Student Example

Relation

```
STD(StudentID,
StudentName,
StudentAddress,
ProgramName,
Credits)
```

FDs

```
StudentID →
StudentName,
StudentAddress,
ProgramName,
Credits
```

Aur

```
ProgramName → Credits
```

Matlab

Agar Student ID pata ho to

Hum us student ka

- Name

- Address

- Program

- Credits

Sab kuch bata sakte hain.

Aur

Program ka naam pata ho

To Credits bhi pata chal jayenge.

---

# Functional Dependency aur Keys

Ab sawal hai

FD ka use kya hai?

Answer

FD ki help se hum

Database ki

# Keys

find karte hain.

---

# Super Key

Aisa attribute ya attributes ka set

Jo har row ko uniquely identify kare.

Example

```
StudentID
```

Agar StudentID unique hai

To

```
StudentID
```

Super Key hai.

---

# Candidate Key

Candidate Key

Minimal Super Key hoti hai.

Matlab

Extra attribute na ho.

Example

```
StudentID
```

Agar akela hi unique hai

To

```
(StudentID, Name)
```

Candidate Key nahi hogi

Kyun?

Kyun ke Name extra hai.

---

# Example

Employee Table

```
EMP(
EmployeeID,
EmployeeName,
Address,
Department,
ProjectID,
ProjectSalary)
```

FDs

```
EmployeeID →
EmployeeName,
Address,
Department
```

Aur

```
EmployeeID,
ProjectID
→
ProjectSalary
```

---

# Armstrong Inference Rules

Ab maan lo kuch Functional Dependencies di hui hain.

Question

Nayi Functional Dependency kaise nikalenge?

Answer

Inference Rules se.

Ye rules

Dr. Armstrong ne diye thay.

Isi liye inhe

**Armstrong Axioms**

kehte hain.

Total

6 Rules hain.

Exam mein bohot important hain.

---

# Rule 1

# Reflexivity

Formula

```
A → B

jab

B subset ho A ka
```

Simple Language

Agar right side already left side ke andar mojood ho

To dependency automatically true hogi.

Example

```
(StudentName,Address)

→

StudentName
```

Ye hamesha true hai.

Isko

**Trivial Dependency**

bhi kehte hain.

---

# Rule 2

# Augmentation

Formula

```
A → B

to

AC → BC
```

Simple Language

Agar dependency sahi hai

To dono sides par same attribute add kar do

Dependency phir bhi sahi rahegi.

Example

```
StudentID

→

StudentName
```

To

```
(StudentID, Address)

→

(StudentName, Address)
```

---

# Rule 3

# Transitivity

Ye bilkul Maths wali property hai.

Formula

```
A → B

B → C

To

A → C
```

Example

```
StudentID

→

Program
```

Aur

```
Program

→

Credits
```

To

```
StudentID

→

Credits
```

---

# Rule 4

# Union (Additivity)

Formula

```
A → B

A → C

To

A → BC
```

Example

```
EmployeeID

→

Name
```

Aur

```
EmployeeID

→

Qualification
```

To

```
EmployeeID

→

Name,
Qualification
```

---

# Rule 5

# Decomposition (Projectivity)

Ye Union ka ulta hai.

Formula

```
A → BC

To

A → B

Aur

A → C
```

Example

```
EmployeeID

→

Name,
Qualification
```

To

```
EmployeeID

→

Name
```

Aur

```
EmployeeID

→

Qualification
```

---

# Rule 6

# Pseudo Transitivity

Formula

```
A → B

CB → D

To

AC → D
```

Ye thodi difficult rule hai.

Sirf formula yaad kar lo.

Exam mein aksar isi tarah poochte hain.

---

# Normalization

Ab sab se important topic

Normalization

---

# Normalization Kya Hai?

Normalization

Database ko organize karne ka process hai.

Iska purpose

Database ko

- Clean banana

- Duplicate data khatam karna

- Errors kam karna

- Storage bachana

- Update asaan banana

---

# Real Life Example

Galat Table

|StudentID|StudentName|Books|
|----------|------------|------|
|101|Ali|B1,B2|

Problem

Books mein

Do values hain.

Database confuse ho jayega.

Isi liye

Normalization use hogi.

---

# First Normal Form (1NF)

Definition

Har row

Har column

Sirf

**One Value**

honi chahiye.

Isko kehte hain

Atomic Value.

---

# Atomic Value Kya Hoti Hai?

Atomic

Matlab

Aik hi value.

Example

✅

```
BookID

B001
```

❌

```
BookID

B001,B002
```

---

# Example (Not 1NF)

|StudentID|Name|BookID|
|----------|------|--------|
|101|Ali|B1,B2|

Problem

BookID mein

2 values hain.

Isliye

Ye

1NF mein nahi hai.

---

# Convert into 1NF

|StudentID|Name|BookID|
|----------|------|--------|
|101|Ali|B1|
|101|Ali|B2|

Ab har row mein sirf aik BookID hai.

Ab table

1NF mein aa gaya.

---

# Second Normal Form (2NF)

Definition

Table

1NF mein bhi ho

Aur

Har non-key attribute

Complete Key par depend kare.

---

# Simple Language

Agar Composite Key hai

To

Data uske sirf aik hissa par depend nahi hona chahiye.

Poori key par depend hona chahiye.

---

# Example

Table

|StudentID|CourseID|StudentName|
|----------|---------|-------------|

Composite Key

```
(StudentID,
CourseID)
```

StudentName sirf StudentID se mil raha hai.

CourseID ki zarurat hi nahi.

Yani

StudentName

Composite key ke sirf aik hissa par depend kar raha hai.

Ye

Partial Dependency

kehlati hai.

Isi wajah se

Ye

2NF mein nahi hai.

Solution

Student table alag bana do.

Course table alag bana do.

---

# Difference Between 1NF and 2NF

## First Normal Form

Focus

```
One Cell

One Value
```

---

## Second Normal Form

Focus

```
No Partial Dependency
```

---

# Exam Tips ⭐

Yaad rakho

```
FD

↓

Keys

↓

Normalization

↓

1NF

↓

2NF

↓

3NF
```

Ye poora flow exam mein bohot poocha jata hai.

---

# Short Revision

## Functional Dependency

Ek attribute doosre attribute ko determine karta hai.

---

## Determinant

Left Side

---

## Dependent

Right Side

---

## Super Key

Unique identifier

---

## Candidate Key

Minimal Super Key

---

## Reflexivity

Subset

---

## Augmentation

Dono side same attribute add karo.

---

## Transitivity

A→B

B→C

To

A→C

---

## Union

Do dependencies ko combine karo.

---

## Decomposition

Ek dependency ko tod do.

---

## Pseudo Transitivity

Formula yaad karo.

---

## Normalization

Duplicate data remove karna.

---

## 1NF

Har cell mein sirf aik value.

---

## 2NF

No Partial Dependency.

---

# Important Interview / Viva Questions

### Q1. Functional Dependency kya hoti hai?

**Answer:** Jab ek attribute ki value se doosre attribute ki value uniquely determine ho jaye to usay Functional Dependency kehte hain.

---

### Q2. Determinant kya hota hai?

**Answer:** Functional Dependency ke left side wala attribute ya attribute set Determinant kehlata hai.

---

### Q3. Dependent kya hota hai?

**Answer:** Functional Dependency ke right side wala attribute Dependent kehlata hai.

---

### Q4. 1NF ka main rule kya hai?

**Answer:** Har row ke har cell mein sirf ek (atomic) value honi chahiye.

---

### Q5. 2NF kab apply hoti hai?

**Answer:** Jab table ki Composite Key ho aur hume Partial Dependency remove karni ho.

---

# Final Summary

Is lecture mein hum ne seekha:

- Functional Dependency kya hoti hai.
- Determinant aur Dependent kya hote hain.
- Super Key aur Candidate Key ka concept.
- Armstrong ke 6 Inference Rules.
- Normalization ka purpose.
- First Normal Form (1NF).
- Second Normal Form (2NF).

💡 **Golden Rule:**  
**Pehle Functional Dependency samjho, phir Keys samjho, uske baad hi Normalization (1NF, 2NF, 3NF...) aasani se samajh aayegi.**
