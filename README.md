

#  Online Exams System – Oracle PL/SQL Project

##  Project
**Course:** (PL/SQL)  
**Student:** Divine Mutuyimana  
**Student ID:** 26855  
**Group:** TUE GRP B  
**Instructor:** Eric Maniraguha  
**Database Username:** Tue_26855_DIVINE_Online_Examination_MS  
**Password:** 1234

---

##  Project Overview
This project involves the **design, implementation, and monitoring** of a PL/SQL-based Oracle database for an **Online Exams System**. It aims to provide a secure and efficient system for managing online tests, users, and results.

---

##  Phase 1 – Requirements & Problem Statement

**Objective:**  
Design a database system that supports:
- User roles: Admin, Instructor, Student
- Exam creation, question management
- Online participation and auto-grading
- Results tracking and audit logging

**Deliverables:**
- Problem Statement Document
- ERD (Entity-Relationship Diagram)
- Entity Descriptions
- Presentation Slides

---

##  Phase 2 – Database Design

**Tasks:**
- Schema design and normalization
- Table creation with constraints
- Data integrity rules and relationships

**Sample Tables:**
- `Users (UserID, Name, Role, Email, Password)`
- `Courses (CourseID, Name, InstructorID)`
- `Exams (ExamID, CourseID, Date, Duration)`
- `Questions (QuestionID, ExamID, Content, Type)`
- `Answers (AnswerID, QuestionID, IsCorrect)`
- `Results (ResultID, StudentID, ExamID, Score)`

---

##  Phase 3 – Implementation (PL/SQL Scripts)

**Components:**
- SQL scripts for schema creation
- Stored procedures and functions
- System triggers and packages
- Sample data inserts for testing

**Tools Used:**
- Oracle SQL Developer
- SQL*Plus

---

##  Phase 4 – Auditing & Security

**Auditing Features:**
- Log user logins and exam submissions
- Use triggers to record audit logs

**Example Trigger:**
```bash
CREATE OR REPLACE TRIGGER trg_exam_submission
AFTER INSERT ON Submissions
FOR EACH ROW
BEGIN
  INSERT INTO Audit_Log (Action, Timestamp, UserID)
  VALUES ('Exam Submitted', SYSDATE, :NEW.StudentID);
END;
```