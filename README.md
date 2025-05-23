 📘 Online Exams System – Oracle PL/SQL Capstone Project

> A complete Oracle PL/SQL-based online exam platform, designed for managing users, exams, submissions, and audit logs. This project demonstrates database design, advanced programming, and enterprise-level monitoring using Oracle Enterprise Manager.

---

## 👨‍🎓 Student Info

- **Student Name:** Divine Mutuyimana  
- **Student ID:** 26855  
- **Group:** TUE GRP B  
- **Instructor:** Eric Maniraguha  
- **Preferred Username:** `Tue_26855_DIVINE_Online_Examination_MS`  
- **Password:** `Divine`

---

## 🧩 Phase 1 – Problem Statement

🎯 **Objective:**  
To develop a robust, secure, and auditable database system for managing online examinations. The system must allow:
- Admin to manage users and structure
- Instructors to create exams and questions
- Students to take exams and get instant results
- Secure logging and audit trail of all activities

---

## 📐 Phase 2 – Database Design

📊 **Entity-Relationship Design & Normalization**

**Core Tables (7 Total):**
| Table         | Purpose |
|---------------|---------|
| `Users`       | Stores user credentials and roles (Student, Instructor, Admin) |
| `Courses`     | Course info linked to instructors |
| `Exams`       | Exam metadata (date, duration, etc.) |
| `Questions`   | Questions for each exam |
| `Answers`     | Possible answers per question with correctness flag |
| `Submissions` | Tracks exam attempts per student |
| `Results`     | Stores calculated scores and outcomes |

---

## 🛠️ Phase 3 – Database Creation & Commands

### 🔐 Database User Setup
```sql
CREATE USER Tue_26855_DIVINE_Online_Examination_MS IDENTIFIED BY Divine;
GRANT DBA TO Tue_26855_DIVINE_Online_Examination_MS;
```

### 💾 Table Creation Sample
```sql
CREATE TABLE Users (
    UserID NUMBER PRIMARY KEY,
    Name VARCHAR2(100),
    Role VARCHAR2(20),
    Email VARCHAR2(100) UNIQUE,
    Password VARCHAR2(50)
);
```

### 🔑 Foreign Key Example
```sql
CREATE TABLE Courses (
    CourseID NUMBER PRIMARY KEY,
    Name VARCHAR2(100),
    InstructorID NUMBER,
    FOREIGN KEY (InstructorID) REFERENCES Users(UserID)
);
```

### 🧮 Sample Data Insert
```sql
INSERT INTO Users VALUES (1, 'Eric Maniraguha', 'Instructor', 'eric@auca.ac.rw', 'password123');
```

---

## 🧠 Phase 4 – PL/SQL Implementation

### 📂 Procedure Example
```sql
CREATE OR REPLACE PROCEDURE Add_Student (
    p_name IN VARCHAR2,
    p_email IN VARCHAR2,
    p_password IN VARCHAR2
) AS
BEGIN
    INSERT INTO Users (UserID, Name, Role, Email, Password)
    VALUES (Users_seq.NEXTVAL, p_name, 'Student', p_email, p_password);
END;
```

### 🌀 Function Example
```sql
CREATE OR REPLACE FUNCTION Calculate_Score (
    p_exam_id IN NUMBER,
    p_student_id IN NUMBER
) RETURN NUMBER IS
    v_score NUMBER;
BEGIN
    SELECT COUNT(*) INTO v_score
    FROM Answers a
    JOIN StudentAnswers sa ON a.AnswerID = sa.AnswerID
    WHERE a.IsCorrect = 1 AND sa.ExamID = p_exam_id AND sa.StudentID = p_student_id;

    RETURN v_score;
END;
```

### ❗ Exception Handling
```sql
BEGIN
    EXECUTE IMMEDIATE 'DROP TABLE Results';
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error dropping Results: ' || SQLERRM);
END;
```

---

## 🔐 Phase 5 – Triggers & Audit Logging

### 📋 Audit Table Example
```sql
CREATE TABLE Audit_Log (
    LogID NUMBER PRIMARY KEY,
    UserID NUMBER,
    Action VARCHAR2(100),
    Timestamp DATE DEFAULT SYSDATE
);
```

### 🔁 Trigger to Log Activity
```sql
CREATE OR REPLACE TRIGGER trg_exam_submission
AFTER INSERT ON Submissions
FOR EACH ROW
BEGIN
    INSERT INTO Audit_Log (UserID, Action)
    VALUES (:NEW.StudentID, 'Submitted Exam');
END;
```

---

## 📊 Phase 6 – Oracle Enterprise Manager (OEM)

🛠️ **OEM Setup Command**
```sql
EXEC DBMS_XDB_CONFIG.SETHTTPSPORT(5500);
```

🔗 **Access URL:**  
`https://localhost:5500/em`

📋 **Features Used:**
- Session & performance monitoring
- Tablespace usage
- SQL history & resource usage

> 🖼️ **Note:** OEM screenshots will be added upon final submission.

---

## 🔍 Phase 7 – Advanced Features

### ⛔ Restriction Triggers (No changes on weekends/public holidays)
```sql
CREATE OR REPLACE TRIGGER trg_block_weekends
BEFORE INSERT OR UPDATE OR DELETE ON Users
BEGIN
    IF TO_CHAR(SYSDATE, 'DY') IN ('SAT', 'SUN') THEN
        RAISE_APPLICATION_ERROR(-20001, 'Changes not allowed on weekends!');
    END IF;
END;
```

### 📊 Analytic Queries (Window Functions)
```sql
SELECT StudentID, ExamID, Score,
       RANK() OVER (PARTITION BY ExamID ORDER BY Score DESC) AS Rank
FROM Results;
```

---

## 🧪 Testing & Validation

✅ **Tested Scenarios**
- Student registration and login
- Instructor creating courses, exams, and questions
- Students submitting exams
- Auto-scoring and ranking
- Restriction enforcement
- OEM performance review

---

## 📁 Project Folder Structure

```
OnlineExamsSystem/
├── sql/
│   ├── create_tables.sql
│   ├── procedures.sql
│   ├── triggers.sql
│   ├── audit_log.sql
│   └── test_queries.sql
├── docs/
│   ├── ERD.pdf
│   ├── Presentation.pptx
│   └── ProblemStatement.pdf
├── screenshots/
│   └── (OEM screenshots to be added)
└── README.md
```

---

## ✅ Final Remarks

This project demonstrates mastery in:
- Relational database design
- PL/SQL programming and triggers
- Audit and security enforcement
- Database performance monitoring with OEM
- Real-world database system simulation

📘 **Grading-Ready:** Everything is formatted for easy review by instructors.

---

> © 2025 Divine Mutuyimana | AUCA | Database Design & Implementation
