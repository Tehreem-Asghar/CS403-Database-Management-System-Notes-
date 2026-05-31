# Lecture 11 - Inheritance, Supertype, Subtype & Constraints (CS403)

# Overview

Is lecture mein hum ne yeh concepts padhe:

- Inheritance
- Supertype
- Subtype
- Supertype/Subtype Relationship
- Constraints
- Completeness Constraint
  - Total Completeness
  - Partial Completeness
- Disjoint Constraint
- Overlapping Constraint
- Subtype Discriminator

---

# Inheritance

Inheritance ka matlab hai kisi parent entity ki properties ka child entities ko transfer hona.

Database systems mein inheritance ka use common attributes ko baar baar likhne se bachane ke liye kiya jata hai.

## Real-Life Example

Agar ek company mein Employees ki different categories hain:

- Salaried Employee
- Hourly Employee

To dono ke paas kuch common information hogi:

- Employee ID
- Employee Name
- Address
- Phone Number

Ye common information Parent Entity mein rakhi jati hai aur Child Entities usay inherit karti hain.

---

# Supertype

Supertype ek general entity hoti hai jo common attributes rakhti hai.

## Example

```text
EMPLOYEE
---------
EmpId
EmpName
EmpAddress
EmpPhNo
```

Yahan EMPLOYEE ek Supertype hai.

---

# Subtype

Subtype Supertype ki specialized form hoti hai.

Subtype:

- Supertype ke tamam common attributes inherit karti hai.
- Apne additional attributes bhi rakhti hai.

## Example

```text
EMPLOYEE
     |
-------------------
|                 |
|                 |
SALARIED       HOURLY
```

---

# Example 1 - Employee Hierarchy

## Supertype

```text
EMPLOYEE
---------
EmpId
EmpName
EmpAddress
EmpPhNo
```

## Subtype 1

```text
SALARIED
---------
Grade
AnnualSalary
```

## Subtype 2

```text
HOURLY
---------
NoOfHours
HourlyRate
```

## Diagram

```text
                    EMPLOYEE
          --------------------------
          EmpId
          EmpName
          EmpAddress
          EmpPhNo
                 |
        ------------------
        |                |
        |                |
    SALARIED         HOURLY
    --------         -------
    Grade            NoOfHours
    AnnualSalary     HourlyRate
```

---

# Real Example

## Salaried Employee

```text
EmpId = E101
EmpName = Ali
EmpAddress = Karachi
EmpPhNo = 03001234567

Grade = A
AnnualSalary = 1200000
```

## Hourly Employee

```text
EmpId = E102
EmpName = Ahmed
EmpAddress = Lahore
EmpPhNo = 03111234567

NoOfHours = 8
HourlyRate = 500
```

---

# Example 2 - Person Hierarchy

## Supertype

```text
PERSON
--------
P_Id
P_Name
P_Address
P_PhNo
```

## Student Subtype

```text
STD
-----
CourseName
CGPA
```

## Faculty Subtype

```text
FAC
-----
Qualification
Grade
```

## Diagram

```text
                    PERSON
          ------------------------
          P_Id
          P_Name
          P_Address
          P_PhNo
                 |
        ------------------
        |                |
        |                |
       STD             FAC
    ---------       --------
    CourseName      Qualification
    CGPA            Grade
```

---

# Supertype / Subtype Relationship

Supertype aur Subtype relationship ka purpose:

- Data duplication kam karna
- Database ko organize karna
- Maintenance aasaan banana
- Clarity improve karna

## Example

Agar PERSON ke attributes:

- P_Id
- P_Name
- P_Address
- P_PhNo

Student aur Faculty dono mein alag alag likhe jayein to duplication hogi.

Inheritance ki wajah se yeh problem solve ho jati hai.

---

# Benefits of Inheritance

## 1. Data Duplication Kam Hoti Hai

Common attributes sirf ek jagah store hote hain.

## 2. Database Clear Rehta Hai

Structure samajhna aasaan ho jata hai.

## 3. Maintenance Easy Ho Jati Hai

Agar supertype mein naya attribute add kiya jaye to subtypes automatically inherit kar leti hain.

---

# Constraints

Supertype aur Subtype relationship par kuch restrictions lagayi jati hain.

In restrictions ko Constraints kehte hain.

Do major constraints hain:

1. Completeness Constraint
2. Disjointness Constraint

---

# Completeness Constraint

Completeness batati hai:

> Supertype ki instances ka Subtypes ke sath kitna relationship hai.

Do types:

1. Total Completeness
2. Partial Completeness

---

# Total Completeness

Definition:

Har Supertype instance kisi na kisi Subtype mein zaroor mojood hogi.

## Diagram

```text
PERSON
  |
-----------
|         |
|         |
STD      FAC
```

## Example

| Person | Student | Faculty |
|----------|----------|----------|
| Ali | ✔ | |
| Ahmed | | ✔ |
| Sara | ✔ | |

Yahan har Person kisi na kisi subtype mein hai.

Isliye Total Completeness hai.

---

# Real-Life Example

University mein:

Har Person ya to:

- Student hai
- Faculty Member hai

Koi Person aisa nahi jo dono mein se kisi bhi category mein na ho.

---

# Partial Completeness

Definition:

Zaroori nahi ke har Supertype instance kisi Subtype mein ho.

## Example

| Person | Student | Faculty |
|----------|----------|----------|
| Ali | ✔ | |
| Ahmed | | ✔ |
| Usman | | |

Usman kisi subtype mein nahi.

Isliye Partial Completeness hai.

---

# Real-Life Example

Vehicle company mein:

Vehicles:

- Car
- Truck
- Bus
- Motorcycle

Agar sirf Car aur Truck ko subtype banaya gaya ho to:

Bus aur Motorcycle sirf Vehicle entity mein rahenge.

Ye Partial Completeness hai.

---

# Disjoint Constraint

Disjoint Constraint batati hai:

> Ek Supertype instance sirf ek hi Subtype mein ja sakti hai.

---

# Employee Example

```text
EMPLOYEE
├── SALARIED
└── HOURLY
```

Rule:

Employee ya to Salaried hoga ya Hourly.

Dono nahi.

---

# Valid Example

| EmpId | Type |
|--------|--------|
| E101 | Salaried |
| E102 | Hourly |

---

# Invalid Example

| EmpId | Salaried | Hourly |
|--------|----------|----------|
| E101 | ✔ | ✔ |

Disjoint Rule violate ho gaya.

---

# Overlapping Constraint

Overlapping Disjoint ka opposite hai.

Definition:

Ek Supertype instance multiple Subtypes mein ho sakti hai.

---

# Employee Example

Maan lo:

Employee:

- Din mein Salaried kaam karta hai.
- Shaam mein Hourly basis par extra duty karta hai.

To uska record:

```text
SALARIED
AND
HOURLY
```

Dono subtypes mein hoga.

---

# Patient Example (Complete + Disjoint)

## Diagram

```text
                    PATIENT
              ----------------
              P_Id
              P_Name
              AdmDate
                    |
                  (D)
                 /   \
                /     \
      OUTDOOR       INDOOR
      PATIENT       PATIENT

Prescription      WardNo
                  DateDischarge
```

## Explanation

Hospital mein patient:

- Ya Indoor hoga
- Ya Outdoor hoga

Dono nahi.

Isliye:

### Completeness

Total Completeness

### Disjointness

Disjoint

---

# Vehicle Example (Partial Completeness)

## Diagram

```text
               VEHICLE
          -----------------
          Veh_Id
          Model
          Registration
                |
          --------------
          |            |
          |            |
         CAR         TRUCK

      NoOfDoors
      Passengers

                  Price
```

## Explanation

Company ke paas:

- Car
- Truck
- Bus
- Van
- Motorcycle

Sab vehicles hain.

Lekin sirf Car aur Truck ko subtype banaya gaya hai.

Baqi vehicles Vehicle entity mein rahenge.

Ye Partial Completeness hai.

---

# Overlapping Example (Parts)

## Diagram

```text
                 PART
            --------------
            Part_No
            PartName
                  |
                 (O)
                /   \
               /     \
     MANUFACTURED   PURCHASED
```

---

# Real-Life Example

Customer ne:

```text
1000 Computer Chips
```

ka order diya.

Company ne:

```text
700 Chips
```

khud manufacture kiye.

Baqi:

```text
300 Chips
```

supplier se purchase kiye.

Ab wohi Part:

✔ Manufactured bhi hai

✔ Purchased bhi hai

Isliye record dono subtypes mein store hoga.

---

# Four Possible Combinations

## 1. Complete Disjoint

- Har instance subtype mein hogi
- Sirf ek subtype mein hogi

Example:

Patient

---

## 2. Complete Overlapping

- Har instance subtype mein hogi
- Multiple subtypes mein ho sakti hai

---

## 3. Partial Disjoint

- Kuch instances subtype mein nahi hongi
- Jo hongi woh sirf ek subtype mein hongi

Example:

Vehicle

---

## 4. Partial Overlapping

- Kuch instances subtype mein nahi hongi
- Jo hongi woh multiple subtypes mein bhi ho sakti hain

---

# Subtype Discriminator

Definition:

Subtype Discriminator ek attribute hota hai jo batata hai ke Supertype ki instance kis Subtype se belong karti hai.

---

# Vehicle Example

Supertype:

```text
VEHICLE
---------
Veh_Id
Model
Vehicle_Type
```

Vehicle_Type:

| Value | Meaning |
|---------|----------|
| C | Car |
| T | Truck |

---

# Example Data

| Veh_Id | Vehicle_Type |
|---------|---------------|
| V101 | C |
| V102 | T |

---

# Overlapping Example

Part Entity:

```text
Manufactured
Purchased
```

Possible Values:

| Manufactured | Purchased | Result |
|-------------|------------|---------|
| Y | Y | Manufactured + Purchased |
| Y | N | Manufactured Only |
| N | Y | Purchased Only |
| N | N | Neither |

---

# Importance of Subtype Discriminator

## 1. Fast Identification

Subtype foran identify ho jati hai.

## 2. Better Searching

Database ko repeatedly scan nahi karna parta.

## 3. Better Performance

Queries fast execute hoti hain.

## 4. Easy Management

Database structure simple aur maintainable rehta hai.

---

# Quick Revision

## Inheritance

Parent entity ki properties child entities ko transfer hona.

## Supertype

General entity jo common attributes rakhti hai.

## Subtype

Specialized entity jo Supertype ke attributes inherit karti hai.

## Total Completeness

Har Supertype instance kisi na kisi Subtype mein zaroor hogi.

## Partial Completeness

Kuch Supertype instances kisi Subtype mein nahi hongi.

## Disjoint Constraint

Ek instance sirf ek Subtype mein hogi.

## Overlapping Constraint

Ek instance multiple Subtypes mein ho sakti hai.

## Subtype Discriminator

Special attribute jo batata hai ke instance kis Subtype se belong karti hai.
