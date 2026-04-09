# 📘 Database Systems - Lecture 01 Notes 

## 📌 Importance of Databases

Databases bohat important hain. Traditionally computer applications do types ki hoti hain:

- **Scientific / Engineering Applications**
- **Commercial / Business Applications**

### 🔬 Scientific Applications
In mein zyada calculations hoti hain, simple se le kar complex tak.  
Examples:
- Space
- Nuclear
- Medicine  

Yeh applications kabhi kabhi ghanton ya dinon tak computations karti hain.

### 💼 Commercial Applications
In mein zyada calculations nahi hoti, balkay:
- Data store hota hai
- Data access hota hai
- Data ko different formats mein present kiya jata hai  

Examples:
- Banks
- Shopping systems
- Billing systems
- Customer services  

👉 Yeh systems hamari daily life ka hissa hain, is liye databases directly ya indirectly har insan se related hain.

---

## 🗂️ Databases ka Role

Databases ka main goal hai:
> **Data ko efficiently manage karna**

Is liye commercial applications mein databases best choice hain.

Aaj kal:
- Scientific applications bhi databases use kar rahi hain

---

## 📁 Traditional File Processing System

![file system diagram ](https://github.com/Tehreem-Asghar/CS403-Database-Management-System-Notes-/blob/main/IMG-20260409-WA0002.jpg)

Yeh pehla computer-based system tha jo business applications ke liye use hota tha.

### 🕰️ Old System (Manual Files)
- Data files mein rakha jata tha
- Bohat slow aur difficult tha
- Time-consuming aur inefficient

### 💻 Computer System
- Processing fast ho gayi
- Lekin naye problems aaye

---

## ⚠️ Problems in File Processing System

### 1. 🔗 Program-Data Interdependence
- Program aur data ek doosre par depend karte hain
- Ek change doosre ko affect karta hai

#### Example:
Agar bill system mein address add karna ho:
- File structure change hoga
- Multiple programs change karne padenge  

👉 Is se unnecessary effort hota hai

---

### 2. ❌ Non-Sharing of Data
- Har system apna data alag store karta hai

#### Problems:
- **Redundancy** → same data repeat hota hai  
- **Inconsistency** → different systems mein data mismatch ho jata hai  

---

## ✅ Advantages of Database System

![Database Diagram](https://github.com/Tehreem-Asghar/CS403-Database-Management-System-Notes-/blob/main/IMG_20260409_105334.png)

Database system mein:
- Data ek hi jagah store hota hai
- DBMS usay manage karta hai

---

### 1. 🔄 Data Sharing
- Same data multiple applications use karti hain
- Duplicate data store nahi hota  

#### Example:
Student ka data:
- Name
- Roll number
- Address  

👉 Ek hi jagah store hota hai

---

### 2. استقلال (Data Independence)
- Data aur programs separate hote hain
- Ek mein change doosre ko affect nahi karta  

---

### 3. 📉 Controlled Redundancy
- Data unnecessary duplicate nahi hota  
- Agar hota bhi hai to controlled hota hai  

---

### 4. ✔️ Better Data Integrity
- Data ki correctness ensure hoti hai  

#### Important:
Agar data galat ho:
- Results galat honge  
- Decisions wrong honge  
- Business fail ho sakta hai  

👉 DBMS ensure karta hai:
- Data valid ho
- Processing reliable ho  

---

## 🧠 Lecture Summary

Is lecture mein hum ne:
- Databases ki importance samjhi  
- File processing system aur uske problems dekhe  
- Database system ke advantages samjhe  

---

## ✏️ Exercises

1. Apne aas paas ki cheezon ka data socho jo store kiya ja sakta hai  
2. Kisi system (jaise Railway Reservation System) mein possible changes list karo  

---

## 🚀 Author
**Tehreem Asghar**
