# CS403 - Lecture 09 Notes (Roman Urdu)
# Relationships in E-R Data Model

## Lecture Overview

Is lecture mein hum ne seekha:

- Relationships in E-R Data Model
- Types of Relationships
- Relationship Symbols
- Roles in Relationships
- Participation (Total & Partial)
- Relationship Cardinalities
- One-to-One Mapping
- Many-to-One Mapping
- Relationship Naming

---

# Relationships

Jab do ya zyada entities identify aur define kar li jati hain, to phir check kiya jata hai ke unke darmiyan koi relationship mojood hai ya nahi.

Relationship kisi bhi do ya zyada entities ke darmiyan association, linkage ya connection ko represent karti hai.

### Simple Definition

> Relationship entities ke darmiyan connection ko show karti hai.

---

## Real-Life Examples

### Example 1

Employee projects par kaam karta hai.

```text
Employee ── Works_On ── Project
```

---

### Example 2

Student class mein enroll hota hai.

```text
Student ── Enrolls ── Class
```

---

### Example 3

Department projects ko manage karta hai.

```text
Department ── Manages ── Project
```

---

# Relationship Components

Har relationship ke 3 important parts hote hain:

## 1. Name

Relationship ka naam jo association ko describe kare.

Examples:

- Enroll
- Works_On
- Manages
- Supervises

---

## 2. Optionality

Batata hai participation optional hai ya mandatory.

### Optional

Entity relationship mein ho bhi sakti hai aur nahi bhi.

### Mandatory

Entity ko relationship mein hona zaroori hai.

---

## 3. Degree

Relationship mein kitni entities involve hain.

Examples:

- Unary → 1 Entity
- Binary → 2 Entities
- Ternary → 3 Entities
- N-ary → N Entities

---

# Relationship Type

Relationship Type relationship ka abstract form hota hai.

Relationship instances ka collection jo same attributes aur structure share karta ho.

### Example

```text
Enroll
```

Is relationship ki instances:

```text
(S1001, CS101)
(S1002, CS101)
(S1003, IT201)
```

Pura collection Relationship Type ko represent karta hai.

---

# Participants

Jo entities relationship mein shamil hoti hain unko Participants kehte hain.

### Example

```text
Student ── Enroll ── Class
```

Participants:

- Student
- Class

---

# Participation

Participation do types ki hoti hai:

## 1. Total Participation

Jab har entity relationship mein participate kare.

### Symbol

Double Line

```text
Employee ══ Works_For ══ Department
```

### Example

Har employee kisi na kisi department mein kaam karta hai.

---

## 2. Partial Participation

Jab kuch entities relationship mein participate karein aur kuch na karein.

### Symbol

Single Line

```text
Supplier ── Supplies ── Part
```

### Example

Kuch parts supplier ke baghair bhi available ho sakte hain.

---

# Roles in Relationships

Roles batate hain ke relationship mein entity kis capacity mein participate kar rahi hai.

### Example

Manager aur Worker

```text
Employee ── Supervises ── Employee
   Manager           Worker
```

Yahan dono entities Employee hain.

Lekin roles alag hain.

- Ek Manager hai
- Ek Worker hai

---

# Naming Relationships

Relationship ka naam meaningful hona chahiye.

### Example

```text
Student ── Enroll ── Class
```

Relationship Name:

```text
Enroll
```

---

Agar proper naam available na ho to abbreviations use kar sakte hain.

### Example

```text
STD_CLS
```

---

# Symbols Used in ER Diagrams

## Entity

Rectangle

```text
+---------+
| Student |
+---------+
```

---

## Relationship

Diamond

```text
      ◇
   Enroll
```

---

## Weak Relationship

Double Diamond

```text
      ◈
   Contains
```

---

## Partial Participation

Single Line

```text
Student ── Enroll ── Class
```

---

## Total Participation

Double Line

```text
Student ══ Enroll ══ Class
```

---

# Types of Relationships

## 1. Unary Relationship

Unary Relationship ko Recursive Relationship bhi kehte hain.

Jab entity khud se linked ho.

### Example

Roommate Relationship

```text
Student ── Roommate ── Student
```

---

### Real-Life Example

Ali aur Ahmed roommates hain.

```text
Ali ←→ Ahmed
```

Dono Student entity ke instances hain.

---

## 2. Binary Relationship

Jab relationship do entities ko connect kare.

### Example

```text
Student ── Enroll ── Class
```

---

### Real-Life Example

Ali Database Class mein enroll hai.

```text
Ali → Database Class
```

---

### Ordered Pair Representation

```text
Enroll = {
(S1001, ART103A),
(S1020, CS201A),
(S1002, CSC201A)
}
```

---

### Explanation

```text
(S1001, ART103A)
```

Matlab:

Student S1001 ne ART103A class enroll ki.

---

# Relationship Set

Pura collection:

```text
{
(S1001, ART103A),
(S1020, CS201A),
(S1002, CSC201A)
}
```

Relationship Set kehlata hai.

---

# Relationship Instance

Har individual pair:

```text
(S1001, ART103A)
```

Relationship Instance kehlata hai.

---

## 3. Ternary Relationship

Jab relationship mein 3 entities involve hon.

### Example

```text
Student ── Class ── Faculty
```

---

### Real-Life Example

Ali Database Class parhta hai jo Sir Ahmed padha rahe hain.

Entities:

- Student = Ali
- Class = Database
- Faculty = Sir Ahmed

---

## 4. N-ary Relationship

Jab relationship mein N entities involve hon.

### Example

```text
Student
Course
Faculty
Department
Semester
```

Sab mil kar ek relationship bana sakte hain.

---

# Relationship Cardinality

Cardinality batati hai ke ek entity doosri entity se kitni baar relate ho sakti hai.

---

## 1. One-to-One (1:1)

Har entity sirf ek entity se related hoti hai.

### Diagram

```text
Person ── Passport
   1         1
```

---

### Real-Life Example

- Ek Person ka ek Passport hota hai.
- Ek Passport ek Person ka hota hai.

---

## Example Table

| Person | Passport |
|----------|----------|
| Ali | P1001 |
| Ahmed | P1002 |

---

# 2. Many-to-One (M:1)

Kai entities ek entity se relate ho sakti hain.

### Diagram

```text
Employee ── Department
    M            1
```

---

### Real-Life Example

Kai employees ek department mein kaam kar sakte hain.

Lekin har employee sirf ek department mein kaam karta hai.

---

## Example Table

| Employee | Department |
|-----------|------------|
| Ali | IT |
| Ahmed | IT |
| Sara | IT |
| Hina | HR |

---

# Difference Between Total and Partial Participation

| Feature | Total Participation | Partial Participation |
|----------|-------------------|----------------------|
| Participation | Sab entities participate karti hain | Kuch entities participate karti hain |
| Symbol | Double Line | Single Line |
| Mandatory | Yes | No |

---

# Difference Between Unary, Binary and Ternary Relationships

| Relationship | Entities Involved | Example |
|-------------|------------------|----------|
| Unary | 1 Entity | Student–Roommate–Student |
| Binary | 2 Entities | Student–Enroll–Class |
| Ternary | 3 Entities | Student–Class–Faculty |
| N-ary | N Entities | Student–Course–Faculty–Department |

---

# Quick Revision

## Relationship

Entities ke darmiyan connection.

---

## Participant

Relationship mein shamil entities.

---

## Role

Relationship mein entity ki responsibility.

---

## Total Participation

Har entity relationship mein zaroor participate kare.

---

## Partial Participation

Kuch entities relationship mein participate karein.

---

## Unary Relationship

Entity ka khud se relationship.

---

## Binary Relationship

2 entities ka relationship.

---

## Ternary Relationship

3 entities ka relationship.

---

## N-ary Relationship

N entities ka relationship.

---

## One-to-One

Ek entity sirf ek entity se relate ho.

---

## Many-to-One

Kai entities ek entity se relate ho sakti hain.

---

# Important Exam Definitions

### Relationship

Entities ke darmiyan association ya connection ko relationship kehte hain.

### Unary Relationship

Jab entity khud se linked ho.

### Binary Relationship

Jab relationship do entities ko connect kare.

### Ternary Relationship

Jab relationship teen entities ko connect kare.

### Cardinality

Relationship ke through ek entity kitni doosri entities se relate ho sakti hai.

### Total Participation

Jab har entity relationship mein participate kare.

### Partial Participation

Jab kuch entities relationship mein participate karein aur kuch na karein.
