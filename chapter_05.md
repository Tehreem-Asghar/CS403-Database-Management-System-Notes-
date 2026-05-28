# Lecture No. 05

## Reading Material
“Database Systems Principles, Design and Implementation” jo Catherine Ricardo ne likhi hai, Maxwell Macmillan. Sections 2.3.2 aur 2.4.

---

# Lecture ka Overview

- Database Application Development Process  
- Preliminary Study of System  
- Database System Designing ke Tools  
- Data Flow Diagrams (DFD)  
- Different Types of Data Flow Diagram  

Database Design aur Database Application Design dono concepts kaafi milte julte hain. Course ke point of view se focus mainly database designing par hai aur un activities par hai jo database design aur uski internal working ke duran perform hoti hain.  

Jo process is lecture mein discuss kiya gaya hai wo database development ka ek clear model show karta hai. Agarche real world mein aur bhi bohat se methods use hote hain, lekin is course mein sirf un steps ko discuss kiya gaya hai jo directly database design aur development se related hain.

---

# Database Application Development Process

Database Application Development Process mein ye stages shamil hoti hain:

- Database Design  
- Application Programs  
- Implementation  

Ye teen stages hamesha separate sequence mein perform nahi hoti. Bohat dafa ye parallel chalti hain.  

Matlab:
- Jab database design chal raha hota hai tabhi application programs bhi develop hona start ho jate hain.
- Jaise screens ka format ya reports ka layout design karna.

Is course ka main focus database design stages par hai.

---

# Database Design

Database design database application development ka sabse important hissa hota hai.  

Database organization ka data store karta hai. Agar database ka design sahi na ho to:
- Queries galat results dein gi
- Errors generate honge
- System efficiently work nahi karega

Is liye database design ko bohat importance di jati hai.

---

# Database Development Process

Database development process aur database application development process basically same concept hain.  

Is process mein wo tamam steps shamil hote hain jo:
- Database Design
- Application Programs
- Implementation

teeno ko cover karte hain.

---

# Preliminary Study

Database design ka pehla phase Preliminary Study hota hai.  

Is phase mein:
- Organization ke tamam sections ko study kiya jata hai
- Different departments ke relations samjhe jate hain
- Information flow analyze kiya jata hai
- Har stage par hone wali processing ko samjha jata hai

## Example
Agar hum University Management System bana rahe hain to:
- Admission Department
- Accounts Department
- Examination Department

ke darmiyan data flow ko samajhna zaroori hoga.

---

# Requirement Analysis

Preliminary study ke baad Requirement Analysis hoti hai.  

Is phase mein:
- Har section ki detailed requirements collect ki jati hain
- Users ka interview liya jata hai
- System observe kiya jata hai
- Activities ko accurately define kiya jata hai

Ek section ka output doosre section ka input ban sakta hai.

## Example
- Accounts Department fee verify karta hai
- Phir Examination Department ko confirmation bheji jati hai

---

# Database Design

Ye development process ka technical phase hota hai.  

Is phase mein:
- Logical database design create hota hai
- Schemas banaye jate hain
- Entities identify hoti hain
- Attributes assign hote hain
- Relationships define kiye jate hain

## Example

### Student Entity
- StudentID
- Name
- Department

### Course Entity
- CourseID
- CourseName

### Relationship
- Student enrolls in Course

---

# Physical Design

Is phase mein logical design ko actual DBMS par implement kiya jata hai.  

Yahan:
- DBMS select kiya jata hai
- Data types define hote hain
- Indexes create hote hain
- File organization decide hoti hai

DBMS choose karna bohat important hota hai kyun ke is mein organization ki financial investment hoti hai.

## Example
- MySQL
- Oracle
- SQL Server

---

# Implementation

Is phase mein application programs develop kiye jate hain jo users ki requirements ko fulfill karte hain.

Different organizations mein applications ki quantity different ho sakti hai.

## Example
University system mein:
- Student Portal
- Teacher Portal
- Admin Panel

alag alag applications ho sakti hain.

---

# Maintenance of Database System

Maintenance ka matlab system ko continuously monitor aur improve karna hota hai.

Is phase mein:
- Errors fix kiye jate hain
- New features add hoti hain
- Applications update ki jati hain
- Performance improve ki jati hai

## Example
Agar result generation mein issue aa raha ho to usay fix kiya jata hai.

---

# Database Development Process — Approach 2

Ek aur alternative development process bhi hota hai jisme kuch phases modify ya merge kiye gaye hote hain.

Is process ke steps ye hain:

- Analyze User Environment  
- Develop Conceptual Model  
- Map Conceptual Model to Logical Model  
- Choose DBMS  
- Develop Physical Design  
- Implement System  
- Test System  
- Operational Maintenance  

---

# Analyze User Environment

Ye phase pehle wale process ki Preliminary Study jaisa hota hai.

Is mein:
- User environment ko analyze kiya jata hai
- User requirements samjhi jati hain

---

# Develop Conceptual Model

Is phase mein:
- Collected information ko conceptual schema mein convert kiya jata hai
- Database ka high-level structure banaya jata hai

---

# Map Conceptual Model to Logical Model

Yahan conceptual model ko logical database structure mein convert kiya jata hai.

## Example
Entities aur relationships ko tables mein convert karna.

---

# Choose DBMS

Is phase mein suitable DBMS select kiya jata hai according to:
- Requirements
- Environment
- Performance needs

---

# Develop Physical Design

Logical design ko physical database structure mein transform kiya jata hai.

Is phase mein:
- Data types
- Indexes
- File structures

define ki jati hain.

---

# Implement System

Users ke liye applications develop ki jati hain.

## Example
- Login System
- Attendance System
- Result System

---

# Test System

System implementation ke baad testing ki jati hai.

Testing ka purpose:
- Errors detect karna
- Incorrect results check karna
- Proper functionality ensure karna

Agar testing na ho to system inconsistent ho sakta hai.

---

# Operational Maintenance

Testing complete hone ke baad periodic maintenance ki jati hai takay system smoothly work karta rahe.

## Maintenance Activities
- Backup lena
- Errors fix karna
- Performance improve karna
- Security updates karna

---

# Tools Used for Database System Development

## Tools kyun use kiye jate hain?

Tools design process ko standard way mein describe karne ke liye use kiye jate hain.  

Agar kisi system ko design karne ke liye koi standard tool available na ho to:
- Har designer apni alag notation use karega
- Ek designer ki notation dusre designer ko samajh nahi aaye gi

Ye misunderstanding aur bhi zyada dangerous ho sakti hai agar dono designers same system par kaam kar rahe hon.  

Tools designer aur user ke darmiyan mutual agreement banane mein bhi help karte hain taake dono ek hi design ko clearly samajh saken.

---

# Data Flow Diagrams (DFD)

Database systems design karne ke liye sabse common tool **Data Flow Diagram (DFD)** hai.  

DFD system ko graphical form mein represent karta hai aur system ki details ko different levels par show karta hai.

DFD:
- Different processes ke darmiyan data ka flow show karta hai
- Simple hota hai
- Complexities ko hide karta hai
- Processes ke links information flow ko describe karte hain

---

# DFD ki Limitations

DFD ki kuch limitations bhi hain:

- Ye decision points ko express nahi karta
- Ye sirf information flow par focus karta hai

---

# DFD mein Use Hone Wale Symbols

DFD mein limited symbols use hote hain.

---

# DATAFLOW

Dataflow ka purpose system mein ek entity se doosri entity tak information ke flow ko show karna hota hai.

Dataflow ko pipelines ki tarah samjha ja sakta hai jinke through information travel karti hai.

Arrow ke upar us data ka naam likha hota hai jo move ho raha hota hai.

## Example
Student Registration Form → Admission Department

---

# DATA STORE

Data Store wo jagah hoti hai jahan data future use ke liye permanently ya temporarily store kiya jata hai.

Isay ek rectangle ki shape se show kiya jata hai jiske dono sides double lines hoti hain.

Data Store ka naam generally noun hota hai jo storage location ya entity ko identify karta hai.

## Example
- Student Record
- Employee Data
- Fee Details

---

# Processes

Processes ko oval ya rounded rectangle se show kiya jata hai.

Process ka kaam incoming data ko transform karke outgoing data banana hota hai.

Jab data ek form se doosri form mein convert hota hai to process symbol use hota hai.

## Example
- Calculate Result
- Verify Fee
- Generate Report

---

# DFD Processes Numbering

DFD mein processes ko numbering di jati hai taake unki identification easy ho.

## Example
- 1.0
- 1.1
- 1.2

---

# External Entities

External entities wo entities hoti hain jo system ke sath interact karti hain.

Ye:
- Data system ko provide kar sakti hain
- Ya system se data receive kar sakti hain

Inki shape rectangle hoti hai.

## Example
- Student
- Teacher
- Bank

---

# Collector

Collector symbol tab use hota hai jab multiple dataflows ek hi point par terminate ho rahe hon.

Ye data convergence ko show karta hai.

## Example
Different departments ka data ek central database mein store hona.

---

# Separator

Separator tab use hota hai jab ek source ka data multiple destinations ki taraf ja raha ho.

## Example
Result data:
- Student ko bhi jaye
- Admin ko bhi jaye
- Examination department ko bhi jaye

---

# Ring Sum Operator

Ring Sum Operator tab use hota hai jab source process ka data connected sinks mein se sirf kisi ek ki taraf flow kare.

## Example
Payment:
- Cash Counter
ya
- Online Payment Gateway

---

# AND Operator

AND Operator tab use hota hai jab source process ka data tamam connected sinks ki taraf jana zaroori ho.

## Example
Student registration data:
- Accounts Department ko bhi jaye
- Examination Department ko bhi jaye
- Library System ko bhi jaye

---

# Types of DFD

DFD ki major types ye hain:

- Context Diagram
- Level 0 Diagram
- Detailed Diagram

---

# Context Diagram

Ye DFD ka sabse basic level hota hai jo system ki minimum details show karta hai.

## Context Diagram ki Properties

- Ismein hamesha sirf ek process hota hai
- Sirf complete system ko represent karta hai
- System ka naam generally noun phrase hota hai
- Internal details show nahi ki jati
- Sirf input/output aur external entities show hoti hain
- Data Stores show nahi kiye jate
- External entities ke darmiyan direct communication show nahi hoti

## Example
University Management System:
- Student data deta hai
- System result generate karta hai

---

# Level 0 Data Flow Diagram

Level 0 DFD poore system ki working ko detail mein describe karta hai.

Ye context diagram ke baad banaya jata hai.

Ismein:
- Multiple processes hote hain
- Multiple external entities ho sakti hain
- Internal working show hoti hai

Designer ko balance maintain karna hota hai:
- Bohat zyada detail diagram ko complex bana degi
- Bohat kam detail understanding ko difficult bana degi

---

# Steps for Creating Level 0 DFD

## 1. Distinct Modules Identify Karna

System ke different modules identify kiye jate hain.

## Example
- Admission Module
- Accounts Module
- Examination Module

---

## 2. Har Module ka DFD Banana

Har module ki internal functionality ko separately show kiya jata hai.

---

## 3. Different DFDs ko Link Karna

Different modules ke darmiyan:
- Entities
- Processes
- Data Stores

ko connect kiya jata hai.

---

## 4. Processes ko Number Dena

Processes ko numbering di jati hai.

Level 0 mein:
- Sirf decimal se pehle wala part important hota hai

Detailed diagram mein:
- 1.0
- 1.1
- 1.2

jaise sub-processes use hote hain.
