# Examination Management System

## Problem Statement
Develop an Examination Management System database using SQL.

---

# Objectives

- Create tables for Student, Exam, and Result
- Apply Primary Key, Foreign Key, and CHECK constraints
- Insert sample records
- Rename a table
- Truncate a table

---

# E-R Diagram

```text
STUDENT
---------
Student_ID (PK)
Student_Name

        |
        | 1
        |
        | M

RESULT
---------
Result_ID (PK)
Student_ID (FK)
Exam_ID (FK)
Marks

        M
        |
        | 1
        |

EXAM
---------
Exam_ID (PK)
Subject_Name
```

---

# SQL Queries

## Create Student Table

```sql
CREATE TABLE Student (
    Student_ID INT PRIMARY KEY,
    Student_Name VARCHAR(50)
);
```

---

## Create Exam Table

```sql
CREATE TABLE Exam (
    Exam_ID INT PRIMARY KEY,
    Subject_Name VARCHAR(50)
);
```

---

## Create Result Table

```sql
CREATE TABLE Result (
    Result_ID INT PRIMARY KEY,
    Student_ID INT,
    Exam_ID INT,
    Marks INT,

    CONSTRAINT fk_student
    FOREIGN KEY (Student_ID)
    REFERENCES Student(Student_ID),

    CONSTRAINT fk_exam
    FOREIGN KEY (Exam_ID)
    REFERENCES Exam(Exam_ID),

    CONSTRAINT chk_marks
    CHECK (Marks BETWEEN 0 AND 100)
);
```

---

# Insert Sample Data

## Insert into Student Table

```sql
INSERT INTO Student VALUES (1, 'Aarya');
INSERT INTO Student VALUES (2, 'Rahul');
```

---

## Insert into Exam Table

```sql
INSERT INTO Exam VALUES (101, 'DBMS');
INSERT INTO Exam VALUES (102, 'Mathematics');
```

---

## Insert into Result Table

```sql
INSERT INTO Result VALUES (1, 1, 101, 85);
INSERT INTO Result VALUES (2, 2, 102, 90);
```

---

# Display Tables

## Student Table

```sql
SELECT * FROM Student;
```

---

## Exam Table

```sql
SELECT * FROM Exam;
```

---

## Result Table

```sql
SELECT * FROM Result;
```

---

# Rename Result Table

```sql
RENAME Result TO Exam_Result;
```

---

# Verify Renamed Table

```sql
SELECT * FROM Exam_Result;
```

---

# Truncate Exam Table

```sql
TRUNCATE TABLE Exam;
```

---

# Verify Exam Table

```sql
SELECT * FROM Exam;
```

---

# Describe Tables

## Describe Student Table

```sql
DESC Student;
```

## Describe Exam Table

```sql
DESC Exam;
```

## Describe Exam_Result Table

```sql
DESC Exam_Result;
```

---

# Constraints Used

| Constraint | Purpose |
|---|---|
| PRIMARY KEY | Uniquely identifies records |
| FOREIGN KEY | Creates relationship between tables |
| CHECK | Restricts marks between 0 and 100 |

---

# Concepts Covered

- Table Creation
- Primary Key
- Foreign Key
- CHECK Constraint
- INSERT Command
- SELECT Command
- RENAME Command
- TRUNCATE Command
- DESC Command

---

# Output

- Student, Exam, and Result tables created successfully
- Sample records inserted
- Result table renamed to Exam_Result
- Exam table truncated successfully

---

