# DBMS Lecture 32 — Application Programs, User Interface & Forms

> **Course:** CS403 Database Management Systems  
> **Lecture:** 32  
> **Main Topics:** Application Programs, User Interface, Forms, User-Friendly Interfaces, User Types, Windows Controls  
> **Purpose:** Easy-to-understand + exam-focused notes with real-life examples

---

## 1. Lecture ka Basic Idea

Ab tak DBMS mein humne ye cheezen parhi:

1. **Conceptual Database Design** — real-world system ko samajh kar us ka conceptual model banana.
2. **Relational Database Design** — data ko tables mein organize karna.
3. **SQL / DML** — database ke data ko insert, update, delete aur retrieve karna.
4. **SQL Server** — SQL commands ko practically use karne ka tool.

### Ab Lecture 32 mein kya seekh rahe hain?

Ab hum ye samjhenge ke:

> **Database ke upar application program kaise kaam karta hai aur user database ke sath kis interface ke through interact karta hai.**

Simple architecture:

```text
User
  ↓
User Interface / Form
  ↓
Application Program
  ↓
SQL Commands
  ↓
Database
```

### Real-Life Example — University System

Student website par:

```text
Roll No: [________]
Password: [________]

        [Login]
```

Student login karta hai.

- **Form/UI** → student se input leta hai
- **Application Program** → input ko process karta hai
- **SQL** → database mein student ko check karta hai
- **Database** → student ka stored data provide karta hai
- **Application** → result screen par show karta hai

---

# 2. Application Program

## Definition

**Application Programs** woh programs/software hote hain jo users ya organization ki requirements ko perform karne ke liye develop kiye jate hain.

Simple words:

> **Application program user ko database ke data par useful work karne ki facility deta hai.**

### Examples

- Student Management System
- Banking Application
- Hospital Management System
- Library Management System
- Shopping Website
- Payroll System
- Inventory System

### Real Example — Library Management System

Library ke database mein ye tables ho sakti hain:

```text
Students
Books
Borrowing
```

Application student ko ye options de sakti hai:

```text
[Search Book]
[Borrow Book]
[Return Book]
[View Fine]
```

User ko directly database tables aur SQL commands likhne ki zarurat nahi hoti.

---

# 3. Application Program Kab Develop Hota Hai?

Application programs:

- database design ke **baad** develop ho sakte hain
- ya database construction ke **parallel** bhi develop kiye ja sakte hain

### Important Point

Tool selection bhi important hai.

Developer apni requirement aur comfort ke according tool select karta hai.

### Example

Web application ke liye:

```text
HTML + CSS + JavaScript + Backend + Database
```

Desktop application ke liye:

```text
C# / Java / Python GUI + Database
```

---

# 4. General Activities in Application Programs

Application program develop karte waqt generally 5 major activities hoti hain:

```text
1. Data Input
2. Editing
3. Display
4. Processing
5. Reports
```

Ab ek ek ko samajhte hain.

---

## 4.1 Data Input

**Data Input** ka matlab hai user se data lena.

### Example — Student Registration

```text
Student Name: [Ali]
Roll No:      [BC123]
Age:          [20]

              [Submit]
```

Yahan user jo information enter karta hai woh **input** hai.

### Real-Life Example

Online admission form:

```text
Name
Father Name
CNIC
Date of Birth
Address
Phone Number
```

Ye sab input hai.

---

## 4.2 Editing

**Editing** ka matlab hai existing data ko modify/update karna.

### Example

Pehle:

```text
Phone = 0300-1111111
```

Baad mein student new number enter karta hai:

```text
Phone = 0312-2222222
```

Ye **editing/updating** hai.

### Real-Life Example

Facebook profile mein:

```text
Old City: Karachi
New City: Hyderabad
```

Profile information edit karna = Editing.

---

## 4.3 Display

**Display** ka matlab hai information ko user ke samne show karna.

### Example

Student result:

```text
Name: Ali
Roll No: 101
Course: CS403
Marks: 82
Grade: A
```

Application database se information lekar screen par display karti hai.

---

## 4.4 Processing

**Processing** ka matlab hai data par operation perform karna.

### Example

Agar marks hain:

```text
English = 80
Math = 75
Computer = 85
```

Application:

```text
Total = 80 + 75 + 85
      = 240
```

Agar total marks 300 hain:

```text
Percentage = 240 / 300 × 100
           = 80%
```

Ye calculation **processing** hai.

### Real-Life Examples

- Total salary calculate karna
- Tax calculate karna
- Student percentage calculate karna
- Shopping cart ka total nikalna
- Hospital bill calculate karna

---

## 4.5 Reports

**Report** processed data ka organized form hota hai jo user ko useful information provide karta hai.

### Example — Monthly Sales Report

```text
--------------------------------
MONTHLY SALES REPORT
--------------------------------
Product       Quantity    Sales
Laptop          20        2,000,000
Mouse          100          250,000
Keyboard        50          300,000
--------------------------------
Total                    2,550,000
```

### Real-Life Examples

- Monthly salary report
- Student result report
- Hospital patient report
- Inventory report
- Bank transaction report

---

# 5. User Interface (UI)

## Definition

**User Interface (UI)** woh medium hai jiske through user computer/system ke sath interact karta hai.

Simple formula:

```text
User ↔ User Interface ↔ System
```

### Examples of UI

- Buttons
- Menus
- Text boxes
- Checkboxes
- Forms
- Search bars
- Login screens

---

# 6. User Interface itna Important Kyun Hai?

User ke point of view se aksar:

> **System ka interface hi system hota hai.**

User normally ye nahi dekh raha hota ke backend mein kitni efficient coding ho rahi hai.

Woh dekhta hai:

- Button kahan hai?
- Data kahan enter karna hai?
- Result kahan milega?
- Error kyun aaya?
- Next step kya hai?

### Good UI ke Benefits

Acha UI:

- learn karna easy banata hai
- use karna easy banata hai
- user ka time save karta hai
- mistakes reduce karta hai
- productivity increase karta hai
- documentation/training ki need kam karta hai

### Bad UI ka Example

Socho login page par:

```text
Username button kahin hidden
Password option unclear
Login button ka naam "Execute"
Error message: "Invalid operation"
```

User confuse ho jayega.

### Good UI

```text
Username: [________]

Password: [________]

[ Login ]
```

Simple aur clear.

---

# 7. Effective User Interface ki Characteristics

Aik effective UI:

### 1. User ke tasks complete karne mein help kare

User ko jo kaam karna hai, interface usko easy banaye.

### 2. User ko unnecessary rules na sikhaye

User ko system ke internal structure ya database tables yaad karne ki zarurat nahi honi chahiye.

### 3. Unexpected behavior na ho

Button dabane par wohi action hona chahiye jo user expect karta hai.

### 4. User ke process ke mutabiq ho

Interface ko user ke working process ke according design karna chahiye.

---

# 8. Types of User Interface

Lecture mein do major types discuss kiye gaye hain:

```text
1. Text-Based User Interface
2. Graphical User Interface (GUI)
```

---

# 9. Text-Based User Interface

Text-based UI mein user keyboard ke through numbers/commands select karta hai.

### Example

```text
Student Management System

1. Add Record
2. Delete Record
3. Enrollment
4. Result Calculation
5. Exit

Enter your choice:
```

Agar user:

```text
1
```

enter kare, to record add hoga.

### Advantages

- Simple
- Kam resources required
- Keyboard based

### Disadvantage

- Beginners ke liye less friendly
- Visual guidance kam hoti hai

### Important Point

Text-based interfaces **aaj kal comparatively kam use hote hain**, especially ordinary end-user database applications mein.

---

# 10. Graphical User Interface (GUI)

GUI ka full form:

> **Graphical User Interface**

Is mein user graphical controls use karta hai:

- Buttons
- Menus
- Text boxes
- Checkboxes
- Radio buttons
- Drop-down lists

GUI ko commonly **Forms** ke through implement kiya jata hai.

### Example

```text
--------------------------------
       STUDENT FORM
--------------------------------

Name:       [____________]

Roll No:    [____________]

Gender:     ○ Male   ○ Female

Course:     [BSSE ▼]

Skills:
☐ HTML
☐ CSS
☐ Python

            [ Submit ]
--------------------------------
```

---

# 11. Forms

## Definition

**Form** application ka aisa interface/page hota hai jo user se input lene ya information display karne ke liye use hota hai.

### Real-Life Examples

- Sign Up Form
- Login Form
- Admission Form
- Employee Form
- Patient Registration Form
- Online Order Form

---

# 12. Types of Forms

Lecture mein do types diye gaye hain:

```text
1. Browser-Based Forms
2. Non-Browser / Simple GUI Forms
```

---

## 12.1 Browser-Based Forms

Ye forms **web browser** mein run hote hain.

Usually web technologies use hoti hain:

- HTML
- CSS
- JavaScript / scripting languages

### Example

Website registration:

```text
Create Account

Name:     [___________]
Email:    [___________]
Password: [___________]

         [Register]
```

Ye browser-based form hai.

### Real-Life Examples

- Google Forms
- Online university admission form
- Facebook signup
- E-commerce checkout form

---

## 12.2 Non-Browser / Simple GUI Forms

Ye forms browser mein nahi, balkay desktop/application environment mein run hote hain.

### Example

```text
Employee Management App

Employee ID: [_______]
Name:        [_______]
Salary:      [_______]

[Save] [Update] [Delete]
```

Aisi application Windows/Desktop environment mein run kar sakti hai.

---

# 13. User-Friendly Interface

## Meaning

**User-friendly interface** aisa interface hai jo user ke liye:

- easy to learn
- easy to use
- clear
- consistent
- predictable

ho.

Lekin ek important concept:

> **Easy for beginner ka matlab zaroori nahi ke expert ke liye bhi fastest ho.**

Isi liye different types of users ki needs consider karni hoti hain.

---

# 14. Types of Users

Lecture mein 3 categories discuss ki gayi hain:

```text
1. Beginners
2. Intermediate Users
3. Experts
```

---

# 15. Beginners

## Beginner kaun hota hai?

Jo user system ko pehli dafa use kar raha ho.

### Beginner ki Needs

- Simple instructions
- Clear buttons
- Introduction
- Guided tour
- Easy navigation

### Example

Aik student pehli baar university LMS open karta hai.

Usko pata nahi:

```text
Assignment kahan submit hota hai?
Quiz kahan hota hai?
Result kahan hai?
```

Acha interface usay clearly options show karega:

```text
Dashboard
Assignments
Quizzes
Results
Help
```

### Important Point

Beginner ko **guidance** chahiye.

> **Beginner → Guidance**

---

# 16. Intermediate Users

## Intermediate user kaun hota hai?

Ye user system ko jaanta hai, lekin kabhi kabhi details bhool jata hai.

### Needs

- Menus
- Help
- Search
- Clear navigation
- Visible available options

### Example

Employee billing system ko jaanta hai.

Usay pata hai invoice kaise create hota hai, lekin kabhi report option bhool sakta hai.

Menu mein:

```text
File
Customers
Invoices
Reports
Help
```

dekh kar usko function yaad aa jata hai.

### Important Point

> **Intermediate → Reminder / Help**

---

# 17. Expert Users

## Expert kaun hota hai?

Expert user:

- system ko deeply jaanta hai
- kya karna hai pata hota hai
- kaise karna hai bhi pata hota hai

Uska focus hota hai:

> **Speed**

### Expert ki Needs

- Keyboard shortcuts
- Fast navigation
- Quick commands
- Customization

### Example

Experienced accountant har action ke liye mouse use karne ke bajaye keyboard shortcuts use kar sakta hai.

### Important Point

> **Expert → Speed / Shortcuts**

---

# 18. Beginner vs Intermediate vs Expert

| User | Main Need | Example |
|---|---|---|
| Beginner | Guidance | First-time LMS user |
| Intermediate | Help/Reminder | Regular office employee |
| Expert | Speed/Shortcuts | Experienced accountant |

### Easy Memory Trick

```text
Beginner     → Learn
Intermediate → Remember
Expert       → Fast
```

---

# 19. Tips for User-Friendly Interface

Ye section exam ke liye **important** hai.

## Tip 1 — Interface simple hona chahiye

User ko required button ya textbox dhoondhne mein problem nahi honi chahiye.

### Bad

```text
Save button hidden inside 4 menus
```

### Good

```text
[ Save ]
```

---

## Tip 2 — User should be in control

User ko feel hona chahiye ke system us ke control mein hai.

Example:

```text
[Save]
[Cancel]
[Back]
[Next]
```

User ko actions control karne ka option hai.

---

## Tip 3 — User Memory ko unnecessary test na karein

User ko bohat sari cheezein yaad karne par majboor nahi karna chahiye.

### Bad

```text
Press F7 to save
```

without any visible help.

### Better

```text
[ Save ]   Shortcut: F7
```

---

## Tip 4 — Consistency

Interface mein same actions ka design aur behavior consistent hona chahiye.

Example:

Agar har form mein Save button bottom-right hai, to har jagah approximately same location/behavior hona useful hai.

---

## Tip 5 — Process-Based Design

Interface ko **user ke process/workflow** ke according design karna chahiye, sirf database table structure ke according nahi.

### Example — Hospital

User ka process:

```text
Register Patient
       ↓
Check Doctor
       ↓
Appointment
       ↓
Treatment
       ↓
Bill
```

Interface bhi is process ko support kare.

User ko ye nahi sochna chahiye:

```text
"Patient table mein pehle data insert karun
ya Appointment table mein?"
```

Ye database designer/developer ka concern hai.

---

# 20. Process-Based vs Data Structure-Based

### Data Structure Based

Developer database tables ko directly user ke samne la de:

```text
Patient Table
Doctor Table
Appointment Table
Bill Table
```

User confuse ho sakta hai.

### Process Based

User ko actual task diya jaye:

```text
[Register Patient]
[Book Appointment]
[Add Treatment]
[Generate Bill]
```

Ye zyada user-friendly approach hai.

### Important Exam Line

> **User interface should be process-based rather than data-structure-based.**

---

# 21. Entities and Relationships

Lecture mein entity aur relationship ka reference bhi aata hai.

### Entity

Real-world object jiske baare mein data store kiya jata hai.

Examples:

```text
Student
Teacher
Course
Book
Patient
Employee
```

### Relationship

Do ya zyada entities ke darmiyan connection.

Example:

```text
Student ---- enrolls in ---- Course
```

Ya:

```text
Patient ---- gets ---- Treatment
```

### Important Point

Application forms ko entities aur unke relationships ke business process ko support karna chahiye.

---

# 22. Windows Controls

Forms mein different **controls** input lene aur output display karne ke liye use hote hain.

Common controls:

```text
Text Box
Button
Check Box
Radio Button
Combo Box
```

---

## 22.1 Text Box

User text ya number enter karta hai.

### Example

```text
Name: [____________]
Age:  [____________]
```

---

## 22.2 Button

Kisi action ko perform karta hai.

### Examples

```text
[Save]
[Delete]
[Submit]
[Login]
[Search]
```

---

## 22.3 Check Box

Multiple options select karne ke liye use hota hai.

### Example

```text
Skills:

☑ HTML
☑ CSS
☐ Java
☑ Python
```

User multiple skills select kar sakta hai.

---

## 22.4 Radio Button

Generally mutually exclusive options ke liye use hota hai — yani normally **ek option** select hota hai.

### Example

```text
Gender:

○ Male
○ Female
```

User aik option choose karega.

---

## 22.5 Combo Box / Drop-Down

Options ki list mein se selection karne ke liye.

### Example

```text
City: [Karachi ▼]
```

Click karne par:

```text
Karachi
Lahore
Islamabad
Multan
Quetta
```

---

# 23. Numbers, Dates and Text

Forms mein user different types ka data enter karta hai.

### Text

```text
Name: [Ali]
```

### Number

```text
Age: [20]
```

### Date

```text
Date of Birth: [15/08/2005]
```

Text boxes commonly input/display ke liye use kiye jate hain, lekin application ko data type ko correctly handle/validate karna chahiye.

### Real Example — Student Form

```text
Name:            [Ali]
Age:             [20]
Date of Birth:   [15/08/2005]
Roll No:         [BC23001]
```

---

# 24. Complete Real-Life Example — Student Management System

Ab puri lecture ko ek example se connect karte hain.

## Step 1 — User Form

```text
------------------------------------
      STUDENT REGISTRATION
------------------------------------

Name:       [____________]

Roll No:    [____________]

Gender:
○ Male
○ Female

Program:
[BS Software Engineering ▼]

Skills:
☐ HTML
☐ CSS
☐ Python

DOB:
[____________]

        [ Register ]
------------------------------------
```

## Step 2 — Application Program

Application:

1. Input receive karegi
2. Validate karegi
3. Data process karegi
4. Database mein save karegi
5. Result display karegi

## Step 3 — Database

Data tables mein store ho sakta hai:

```text
STUDENT

StudentID
Name
RollNo
Gender
Program
DOB
```

## Step 4 — Display

Save hone ke baad:

```text
Student registered successfully!
Roll No: BC23001
```

## Step 5 — Report

Application:

```text
Total Students = 500
BSSE Students = 180
BSE Students  = 150
BSCS Students = 170
```

ki report generate kar sakti hai.

---

# 25. Complete Flow of an Application

Ek typical database application ka flow:

```text
                 USER
                   ↓
             FORM / UI
                   ↓
          APPLICATION PROGRAM
                   ↓
        VALIDATION / PROCESSING
                   ↓
                SQL
                   ↓
              DATABASE
                   ↓
             RESULT DATA
                   ↓
               DISPLAY
                   ↓
                REPORT
```

Is flow ko yaad karna useful hai.

---

# 26. Important Terms at a Glance

| Term | Simple Meaning |
|---|---|
| Application Program | User ki requirements perform karne wala software |
| User Interface | User aur system ke darmiyan interaction medium |
| GUI | Graphical User Interface |
| Form | Input/output ke liye interface |
| Text-Based UI | Keyboard/command based interface |
| Browser-Based Form | Web browser mein chalne wala form |
| Non-Browser Form | Desktop/simple GUI form |
| Input | User se data lena |
| Editing | Existing data modify karna |
| Display | Data show karna |
| Processing | Data par operations/calculations |
| Report | Organized information/output |
| User-Friendly | Easy to learn and use |
| Beginner | New user |
| Intermediate | Regular but not expert user |
| Expert | Experienced/fast user |
| Control | Form ka UI element |

---

# 27. Exam-Oriented Short Questions

## Q1. What is an application program?

**Answer:**  
Application program is a software program developed to perform the requirements/tasks of users or organizations.

---

## Q2. Write general activities performed by application programs.

**Answer:**

1. Data Input
2. Editing
3. Display
4. Processing
5. Reports

---

## Q3. What is User Interface?

**Answer:**  
User Interface is the medium through which a user interacts with a computer system/application.

---

## Q4. What are the two major types of user interfaces?

**Answer:**

1. Text-Based User Interface
2. Graphical User Interface (GUI)

---

## Q5. What is GUI?

**Answer:**  
GUI stands for Graphical User Interface. It allows users to interact with a system through graphical controls such as buttons, text boxes, menus and checkboxes.

---

## Q6. What are forms?

**Answer:**  
Forms are interfaces used in application programs to take input from users or display information.

---

## Q7. What are two types of forms?

**Answer:**

1. Browser-Based Forms
2. Non-Browser/Simple GUI Forms

---

## Q8. What is a user-friendly interface?

**Answer:**  
A user-friendly interface is an interface that is easy to learn, easy to use, clear, consistent and supports the user's tasks.

---

## Q9. Name the three types of users.

**Answer:**

1. Beginners
2. Intermediate Users
3. Experts

---

## Q10. What does a beginner user need?

**Answer:**  
A beginner needs simple instructions, guidance, clear navigation and introductory help.

---

## Q11. What does an intermediate user need?

**Answer:**  
An intermediate user mainly needs menus, reminders and online/help support.

---

## Q12. What does an expert user need?

**Answer:**  
An expert user needs speed, shortcuts, keyboard navigation and customization.

---

## Q13. What is process-based interface design?

**Answer:**  
It means designing the interface according to the user's work process/tasks rather than directly exposing database tables or data structures.

---

## Q14. Name common Windows controls.

**Answer:**

- Text Box
- Button
- Check Box
- Radio Button
- Combo Box

---

# 28. Important Long Question

## Q. Explain types of users in a user-friendly interface.

### Answer:

There are three major types of users:

**1. Beginners:**  
They are new to the system and need guidance, introductory information and simple instructions.

**2. Intermediate Users:**  
They know the system but may forget details. Menus and help facilities are useful for them.

**3. Expert Users:**  
They know what and how to do the task and mainly want speed. Keyboard shortcuts and customization are useful for them.

### Memory:

```text
Beginner     → Guidance
Intermediate → Help
Expert       → Speed
```

---

# 29. Important Long Question

## Q. Explain general activities of application programs.

### Answer:

Application programs normally perform five general activities:

```text
1. Data Input
2. Editing
3. Display
4. Processing
5. Reports
```

**Data Input:** Taking data from the user.  
**Editing:** Modifying existing data.  
**Display:** Showing data to the user.  
**Processing:** Performing calculations or operations on data.  
**Reports:** Presenting organized information.

### Real Example

In a student management system:

```text
Input     → Student enters marks
Editing   → Marks are corrected
Processing→ Percentage is calculated
Display   → Result is shown
Report    → Class result report generated
```

---

# 30. Most Important MCQ Concepts

### 1. UI stands for:

**User Interface**

### 2. GUI stands for:

**Graphical User Interface**

### 3. Which interface uses keyboard numbers/commands?

**Text-Based UI**

### 4. Which interface is commonly implemented through graphical forms?

**GUI**

### 5. Which user mainly wants speed?

**Expert**

### 6. Which user mainly needs guidance?

**Beginner**

### 7. Which user benefits from menus and reminders?

**Intermediate**

### 8. Which control is used for multiple selections?

**Check Box**

### 9. Which control is normally used to select one option from a group?

**Radio Button**

### 10. Which control allows selection from a list?

**Combo Box**

### 11. Which activity means modifying existing data?

**Editing**

### 12. Which activity means calculating or operating on data?

**Processing**

### 13. Which form runs in a web browser?

**Browser-Based Form**

---

# 31. One-Page Final Revision

Paper se just pehle ye section revise karo:

```text
APPLICATION PROGRAM
↓
User/organization ki requirements perform karne wala software.

GENERAL ACTIVITIES
↓
Input
Editing
Display
Processing
Reports

USER INTERFACE
↓
User aur system ke interaction ka medium.

TYPES OF UI
↓
1. Text-Based
2. GUI

FORMS
↓
1. Browser-Based
2. Non-Browser / Simple GUI

USER TYPES
↓
Beginner     → Guidance
Intermediate → Help / Reminder
Expert       → Speed / Shortcuts

USER-FRIENDLY TIPS
↓
Simple
Consistent
User in control
Less memory burden
Process-based

WINDOWS CONTROLS
↓
Text Box   → Input text/number
Button     → Perform action
Check Box  → Multiple selections
Radio Btn  → One option
Combo Box  → Select from list
```

---

# 32. Super Easy Memory Trick

### Application Activities:

**I E D P R**

```text
I = Input
E = Editing
D = Display
P = Processing
R = Reports
```

### User Types:

**B I E**

```text
B = Beginner → Guidance
I = Intermediate → Help
E = Expert → Speed
```

### Controls:

**T B C R C**

```text
T = Text Box
B = Button
C = Check Box
R = Radio Button
C = Combo Box
```

---

# 33. Final Concept

Lecture 32 ka main idea ye hai:

> **Database sirf data store karta hai. Application program aur user interface user ko database ke sath easily interact karne ka tareeqa dete hain.**

Ek complete system mein:

```text
User
  ↓
UI / Form
  ↓
Application
  ↓
SQL
  ↓
Database
  ↓
Processing
  ↓
Display / Report
```

### Golden Line for Exam

> **A good user interface should help users accomplish their tasks easily, consistently and efficiently without forcing them to understand the underlying database structure.**

---

# Quick Preparation Strategy for Paper

Agar time bohat kam hai to is order mein revise karo:

```text
1. Application Program definition
2. 5 General Activities
3. User Interface definition
4. Text-Based vs GUI
5. Forms ke 2 types
6. Beginner / Intermediate / Expert
7. User-Friendly Interface tips
8. Windows Controls
9. Process-Based Design
```

**Sab se zyada important:** Definitions + types + differences + examples + user categories.
