# Lecture No. 07 — Entity Relationship (E-R) Data Model Detailed Notes

# Overview

Is lecture mein hum ne E-R (Entity Relationship) Data Model ko detail mein padha.  
E-R model database ki conceptual design banane ke liye use hota hai.

Is lecture ke major topics:

- Entity
- Types of Entities
- Attributes
- Types of Attributes
- Domain of Attribute
- E-R Diagram Symbols

---

# Entity Relationship (E-R) Data Model

E-R Data Model ek semantic data model hai jo database ki conceptual design ko graphical form mein represent karta hai.

Ye model:
- easy to understand hota hai
- database design ko clear banata hai
- implementation se independent hota hai

Yani E-R model ko baad mein kisi bhi DBMS:
- MySQL
- Oracle
- SQL Server

mein convert kiya ja sakta hai.

---

# Why We Use E-R Model?

Direct relational model mein design banana difficult aur less expressive hota hai.

E-R model:
- zyada readable hota hai
- relationships ko clear show karta hai
- documentation easy banata hai

Isliye pehle conceptual design E-R model mein banti hai.

---

# Main Constructs of E-R Model

E-R model ke 3 major constructs hote hain:

1. Entity
2. Attribute
3. Relationship

---

# Entity

Entity koi bhi real world object hota hai jiske bare mein hum data store karna chahte hain.

Ye:
- person
- place
- object
- event
- concept

kuch bhi ho sakta hai.

---

# Examples of Entity

| Real World Object | Entity |
|---|---|
| Student | STUDENT |
| Teacher | TEACHER |
| Book | BOOK |
| Car | CAR |
| Employee | EMPLOYEE |

---

# Meanings of Entity

Entity word 3 meanings mein use hota hai:

1. Entity Type
2. Entity Instance
3. Entity Set

---

# 1. Entity Type

Entity Type similar properties wale objects ka group hota hai.

## Example

### STUDENT

Properties:
- Name
- Roll Number
- Age

### EMPLOYEE

Properties:
- Employee ID
- Salary
- Designation

---

# Real Life Example

Agar university ka system hai to:
- STUDENT
- TEACHER
- COURSE

entity types honge.

---

# 2. Entity Instance

Entity type ka specific object entity instance hota hai.

## Example

Entity Type:
```text
STUDENT
```

Instances:
- Ali
- Ahmed
- Sara

---

# Example Table

| Entity Type | Entity Instance |
|---|---|
| STUDENT | Ali |
| STUDENT | Ahmed |
| EMPLOYEE | Bilal |

---

# 3. Entity Set

Kisi entity type ke tamam instances ka collection entity set kehlata hai.

## Example

- All students
- All teachers
- All employees

---

# Strong and Weak Entity Types

Entity types do categories mein divide hoti hain:

1. Strong Entity
2. Weak Entity

---

# Strong Entity

Jo independently exist kar sake.

## Example

### EMPLOYEE

Employee apni identification rakhta hai:
- Employee ID
- Name

Isliye ye strong entity hai.

---

# Weak Entity

Jo kisi doosri entity ke bina exist na kar sake.

## Example

### DEPENDENT

Employee ka dependent:
- employee ke bina exist nahi kar sakta

Agar employee delete ho jaye to dependent bhi delete hoga.

---

# Example

| Employee | Dependent |
|---|---|
| Ali | Wife |
| Ahmed | Son |

Yahan:
- EMPLOYEE = Strong Entity
- DEPENDENT = Weak Entity

---

# Symbols of Entity Types

| Entity Type | Symbol |
|---|---|
| Strong Entity | Single Rectangle |
| Weak Entity | Double Rectangle |

---

# Attribute

Attribute entity ki property hoti hai.

## Example

### STUDENT Entity

Attributes:
- Student ID
- Name
- Age
- Address

---

# Important Point

Entity type ke sab instances ke attributes same hote hain.

Lekin values different ho sakti hain.

---

# Example

| Name | Father Name | Age |
|---|---|---|
| Ali | Ahmed | 20 |
| Sara | Khan | 22 |

---

# Attribute Naming Convention

Attribute names:
- unique hone chahiye
- meaningful hone chahiye

## Examples

| Attribute Name | Meaning |
|---|---|
| empName | Employee Name |
| stAddress | Student Address |
| empSalary | Employee Salary |

---

# Domain of Attribute

Domain possible values ka set hota hai jo attribute le sakta hai.

---

# Example

## Salary Attribute

Agar salary attribute hai to:
- sirf numeric values allowed hongi

Valid:
```text
25000
```

Invalid:
```text
Reema
```

---

# Range Constraint

Salary:
- minimum limit
- maximum limit

bhi rakhi ja sakti hai.

## Example

```text
Salary = 10000 to 200000
```

---

# Benefits of Domain

Domain:
- database integrity maintain karta hai
- invalid data ko rokta hai
- mistakes reduce karta hai

---

# Common Data Types

| Data Type | Description |
|---|---|
| Integer | Whole numbers |
| Float | Decimal numbers |
| Char | Single character |
| Varchar | Variable length text |
| String | Text |

---

# Symbol for Attribute

Attribute ko:
- Oval shape

se represent kiya jata hai.

---

# Types of Attributes

Attributes different types ke hote hain:

1. Simple Attribute
2. Composite Attribute
3. Single-Valued Attribute
4. Multi-Valued Attribute
5. Stored Attribute
6. Derived Attribute

---

# 1. Simple Attribute

Jo further divide na ho sake.

## Examples

- Name
- Age
- Gender

---

# Real Life Example

```text
stName = Ali
```

Ye simple attribute hai.

---

# 2. Composite Attribute

Jo multiple parts par mushtamil ho.

## Example

### Address

Address ke parts:
- House Number
- Street
- City
- Postal Code

---

# Real Life Example

```text
Address
 ├── House No
 ├── Street
 ├── City
 └── Postal Code
```

---

# 3. Single-Valued Attribute

Jiski sirf ek value ho.

## Examples

- CNIC
- Gender
- Date of Birth

---

# 4. Multi-Valued Attribute

Jiski multiple values ho sakti hain.

## Example

### Student Hobbies

Aik student ki hobbies:
- Cricket
- Reading
- Gaming

---

# Employee Skills Example

Employee skills:
- JavaScript
- React
- SQL

---

# 5. Stored Attribute

Jo directly database mein save hota hai.

## Examples

- Name
- Date Of Birth
- Salary

---

# 6. Derived Attribute

Jo calculate hota hai.

## Example

Agar:
```text
DateOfBirth
```

stored hai to:
```text
Age
```

calculate ki ja sakti hai.

---

# Derived Attribute Ka Benefit

- Accurate value milti hai
- Manual updates ki zarurat nahi hoti

---

# Symbols for Different Attributes

| Attribute Type | Symbol |
|---|---|
| Simple | Single Oval |
| Composite | Oval with sub-ovals |
| Multi-Valued | Double Oval |
| Derived | Dashed Oval |

---

# Complete Real Life Example

# University Database System

## Entities

### STUDENT
Attributes:
- Roll Number
- Name
- Age
- Address
- Hobbies

### TEACHER
Attributes:
- Teacher ID
- Name
- Qualification

### COURSE
Attributes:
- Course ID
- Course Name
- Credit Hours

---

# Example of Composite Attribute

## Student Address

```text
Address
 ├── House No
 ├── Street
 ├── Area
 └── City
```

---

# Example of Multi-Valued Attribute

## Skills

```text
Employee Skills:
- JavaScript
- Python
- Database
```

---

# Example of Derived Attribute

```text
Age = Current Date - Date Of Birth
```

---

# Real World Perspective Example

## Fan Example

### Manufacturer Perspective

Important properties:
- Material
- Wire Thickness
- Manufacturing Cost

### Shopkeeper Perspective

Important properties:
- Company Name
- Retail Price
- Color

### Customer Perspective

Important properties:
- Warranty
- Purchase Date
- Dealer Name

---

# Abstraction

Entity types aur unki properties identify karne ke process ko abstraction kehte hain.

---

# Difference Between External Entity and Entity Type

| External Entity | Entity Type |
|---|---|
| Data send/receive karti hai | Similar objects ka group |
| DFD mein use hoti hai | E-R diagram mein use hoti hai |

---

# Important Notes

- Entity real world object hoti hai
- Attribute entity ki property hoti hai
- Domain valid values define karta hai
- Weak entity independent nahi hoti
- Derived attribute calculate hota hai

---

# Short Summary Table

| Concept | Meaning |
|---|---|
| Entity | Real world object |
| Entity Type | Similar objects ka group |
| Entity Instance | Specific object |
| Entity Set | Instances ka collection |
| Attribute | Entity ki property |
| Domain | Possible values |
| Strong Entity | Independent entity |
| Weak Entity | Dependent entity |
| Simple Attribute | Single part |
| Composite Attribute | Multiple parts |
| Multi-Valued | Multiple values |
| Derived Attribute | Calculated value |

---

# Practice Exercises

## Exercise 1

Apne:
- school
- university
- office
- home

environment se:
- entity types identify karein
- attributes identify karein

---

## Exercise 2

University system ka E-R model banayein.

Entities:
- STUDENT
- COURSE
- TEACHER

Unke attributes bhi identify karein.

---

# Conclusion

Is lecture mein hum ne:
- Entity
- Entity Types
- Entity Sets
- Strong & Weak Entities
- Attributes
- Types of Attributes
- Domain

ko detail mein padha.

Next lecture mein:
```text
Relationships
```

discuss ki jayengi.
