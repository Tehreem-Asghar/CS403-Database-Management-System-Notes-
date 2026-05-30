# Lecture 08 - Attributes and Keys (Roman Urdu Notes)

# Introduction

Database mein data ko organize aur identify karne ke liye **Attributes** aur **Keys** ka concept bohat important hota hai.

Attributes kisi entity ki information ko represent karte hain jab ke Keys kisi specific record ko identify karne ke liye use hoti hain.

---

# Attributes

## Definition

Attribute kisi entity ki woh property ya information hoti hai jo usay describe karti hai.

Simple words mein:

> Attribute entity ke bare mein information provide karta hai.

---

## Real Life Example

### Student Entity

| Attribute | Value |
|------------|----------|
| RegNo | SP23-001 |
| Name | Ali |
| Father Name | Ahmed |
| Address | Karachi |
| Phone | 03001234567 |

Yahan:

- RegNo attribute hai
- Name attribute hai
- Address attribute hai
- Phone attribute hai

Ye sab mil kar Student entity ko describe kar rahe hain.

---

# Required and Optional Attributes

## Required Attribute

Aisa attribute jis ki value har record ke liye zaroori ho.

### Example

Student Registration Number

Har student ka registration number hona lazmi hai.

| RegNo |
|---------|
| SP23-001 |

Agar RegNo na ho to student identify nahi ho sakta.

---

## Optional Attribute

Aisa attribute jis ki value ho bhi sakti hai aur nahi bhi.

### Example

Second Phone Number

| Name | Phone2 |
|---------|----------|
| Ali | NULL |

Phone2 optional hai.

---

# Keys

## Definition

Key attributes ka aisa set hota hai jo kisi entity ke specific record ko identify kar sake.

Simple words mein:

> Key kisi record ki unique pehchan hoti hai.

---

# Real Life Example

Sochiye NADRA ke paas Pakistan ke tamam citizens ka data mojood hai.

Agar hamein Ali ko search karna ho to:

❌ Name use nahi kar sakte

Kyunkay Pakistan mein bohat se Ali ho sakte hain.

✔ CNIC use kar sakte hain

Kyunkay har shakhs ka CNIC unique hota hai.

Example:

| CNIC | Name |
|---------|---------|
| 42101-1234567-1 | Ali |
| 42101-7654321-2 | Ali |

Dono ka naam same hai lekin CNIC different hai.

---

# Types of Keys

1. Super Key
2. Candidate Key
3. Primary Key
4. Alternate Key
5. Secondary Key
6. Foreign Key

---

# 1. Super Key

## Definition

Super Key attributes ka aisa set hota hai jo kisi record ko uniquely identify kar sake.

---

## Student Entity Example

| RegNo | Name | Father Name |
|---------|---------|--------------|
| SP23-001 | Ali | Ahmed |
| SP23-002 | Sara | Aslam |

Yahan:

### Super Keys

- RegNo
- RegNo + Name
- RegNo + FatherName
- RegNo + Name + FatherName

Sab Super Keys hain.

Kyunkay in sab combinations mein RegNo mojood hai.

Aur RegNo akela hi record ko uniquely identify kar sakta hai.

---

## Important Point

Agar koi attribute Super Key hai to us ke sath koi bhi extra attribute add kar dein to woh bhi Super Key hi rahe gi.

Example:

RegNo

RegNo + Name

RegNo + Address

RegNo + Phone

Sab Super Keys hain.

---

# 2. Candidate Key

## Definition

Candidate Key woh minimal Super Key hoti hai jiska koi subset Super Key na ho.

Ya:

> Minimal Super Key = Candidate Key

---

## Example

Student Entity

### Super Key

RegNo + Name

Agar Name remove kar dein:

RegNo

Phir bhi record uniquely identify ho jata hai.

Is liye:

RegNo + Name

Candidate Key nahi hai.

---

### Candidate Key

RegNo

Kyunkay:

- Unique identify karta hai
- Is se koi aur attribute remove nahi kiya ja sakta

Is liye RegNo Candidate Key hai.

---

## Important Point

Har Candidate Key Super Key hoti hai.

Lekin har Super Key Candidate Key nahi hoti.

---

# Super Key vs Candidate Key

| Feature | Super Key | Candidate Key |
|----------|------------|---------------|
| Unique Identification | Yes | Yes |
| Minimal | No | Yes |
| Extra Attributes | Ho sakte hain | Nahi |

Example:

### Super Key

RegNo + Name

### Candidate Key

RegNo

---

# 3. Primary Key (PK)

## Definition

Candidate Keys mein se jo key database designer choose kare use Primary Key kehte hain.

---

## Example

Student Entity

| RegNo | CNIC |
|---------|---------|
| SP23-001 | 42101-1234567-1 |

Yahan:

- RegNo Candidate Key hai
- CNIC Candidate Key hai

Database Designer RegNo choose kar leta hai.

To:

### Primary Key

RegNo

### Alternate Key

CNIC

---

## Characteristics of Primary Key

### Unique

Har value unique hogi.

✔ SP23-001

✔ SP23-002

❌ Same RegNo do students ko nahi diya ja sakta.

---

### Cannot be NULL

Primary Key kabhi NULL nahi ho sakti.

Example:

| RegNo |
|---------|
| NULL |

Ye allowed nahi hai.

---

# 4. Alternate Key

## Definition

Jo Candidate Keys Primary Key select nahi hoti unhen Alternate Keys kehte hain.

---

## Example

Candidate Keys:

- RegNo
- CNIC

Primary Key:

- RegNo

Alternate Key:

- CNIC

---

## Shortcut

Candidate Key - Primary Key = Alternate Key

---

# 5. Secondary Key

## Definition

Aisa attribute jis ki value ki bunyaad par records search kiye jayein lekin unique result milna zaroori na ho.

---

## Example

Student Table

| RegNo | Name | City |
|---------|---------|---------|
| 001 | Ali | Karachi |
| 002 | Sara | Karachi |
| 003 | Ahmed | Lahore |

Agar hum Karachi search karein:

Result:

- Ali
- Sara

Do records mil gaye.

City unique nahi thi.

Is liye City Secondary Key hai.

---

## Important Point

Secondary Key:

❌ Unique hona zaroori nahi

Super Key:

✔ Hamesha unique

Candidate Key:

✔ Hamesha unique

Primary Key:

✔ Hamesha unique

Alternate Key:

✔ Hamesha unique

---

# 6. Foreign Key

## Definition

Foreign Key aik table mein mojood aisa attribute hota hai jo kisi doosri table ki Primary Key ko reference karta hai.

---

## Example

### Student Table

| StudentID | Name |
|------------|---------|
| 1 | Ali |
| 2 | Sara |

Primary Key:

StudentID

---

### Fee Table

| FeeID | StudentID | Amount |
|---------|------------|----------|
| 101 | 1 | 5000 |
| 102 | 2 | 5000 |

Yahan:

Fee table ka StudentID

Foreign Key hai.

Kyunkay yeh Student table ki Primary Key ko reference kar raha hai.

---

# Complete Relationship of Keys

```

Super Key
↓
Candidate Key
↓
Primary Key

```

Aur:

```

Candidate Key - Primary Key
=
Alternate Key

```

---

# Easy Real Life Example (University)

| Attribute | Type |
|------------|----------|
| RegNo | Primary Key |
| CNIC | Alternate Key |
| RegNo + Name | Super Key |
| RegNo | Candidate Key |
| City | Secondary Key |

---

# Quick Revision

## Attribute

Entity ki property

Example:

- Name
- Age
- Address

---

## Super Key

Unique identify kare.

Example:

RegNo

RegNo + Name

---

## Candidate Key

Minimal Super Key

Example:

RegNo

---

## Primary Key

Selected Candidate Key

Example:

RegNo

---

## Alternate Key

Remaining Candidate Key

Example:

CNIC

---

## Secondary Key

Searching ke liye use hoti hai

Example:

City

---

## Foreign Key

Do tables ko connect karti hai

Example:

StudentID

---

# Important Exam Points

### Super Key

Unique identify karti hai.

### Candidate Key

Minimal Super Key hoti hai.

### Primary Key

Selected Candidate Key hoti hai.

### Alternate Key

Jo Candidate Key select na ho.

### Secondary Key

Searching ke liye use hoti hai.

### Foreign Key

Tables ke darmiyan relationship create karti hai.
