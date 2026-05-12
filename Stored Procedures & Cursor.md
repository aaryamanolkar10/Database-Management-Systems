# Stored Procedures & Functions using Cursors

## Aim
To perform Stored Procedure and Function operations using Cursors on the Student Database System.

---

# What is a Cursor?

A Cursor is used to fetch records one by one from a table.

- SELECT → displays all rows together
- CURSOR → reads rows one at a time

---

# Tables Used

## Department
- Dept_ID
- Dept_Name
- Budget

## Student
- Student_ID
- Name
- Dept_ID

## Course
- Course_ID
- Course_Name

## Enrollment
- Student_ID
- Course_ID
- Marks

## Faculty
- Faculty_ID
- Faculty_Name
- Dept_ID

---

# Step 1: Create Tables

```sql
CREATE TABLE Department (
    Dept_ID INT PRIMARY KEY,
    Dept_Name VARCHAR(50),
    Budget DECIMAL(10,2)
);

CREATE TABLE Student (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Dept_ID INT,
    FOREIGN KEY (Dept_ID) REFERENCES Department(Dept_ID)
);

CREATE TABLE Course (
    Course_ID INT PRIMARY KEY,
    Course_Name VARCHAR(50)
);

CREATE TABLE Enrollment (
    Student_ID INT,
    Course_ID INT,
    Marks INT,
    FOREIGN KEY (Student_ID) REFERENCES Student(Student_ID),
    FOREIGN KEY (Course_ID) REFERENCES Course(Course_ID)
);

CREATE TABLE Faculty (
    Faculty_ID INT PRIMARY KEY,
    Faculty_Name VARCHAR(50),
    Dept_ID INT,
    FOREIGN KEY (Dept_ID) REFERENCES Department(Dept_ID)
);
```

---

# Step 2: Insert Records

```sql
INSERT INTO Department VALUES (1, 'Computer', 500000);
INSERT INTO Department VALUES (2, 'Mechanical', 300000);

INSERT INTO Student VALUES (101, 'Aarya', 1);
INSERT INTO Student VALUES (102, 'Rahul', 2);
INSERT INTO Student VALUES (103, 'Sneha', 1);

INSERT INTO Course VALUES (201, 'DBMS');
INSERT INTO Course VALUES (202, 'Java');

INSERT INTO Enrollment VALUES (101, 201, 85);
INSERT INTO Enrollment VALUES (102, 201, 35);
INSERT INTO Enrollment VALUES (103, 202, 92);

INSERT INTO Faculty VALUES (1, 'Dr. Sharma', 1);
INSERT INTO Faculty VALUES (2, 'Prof. Mehta', 2);
```

---

# 1. Display All Student Records Using Cursor

```sql
CREATE OR REPLACE PROCEDURE Show_Students
AS
    CURSOR c_student IS
        SELECT * FROM Student;

    s_id Student.Student_ID%TYPE;
    s_name Student.Name%TYPE;
    s_dept Student.Dept_ID%TYPE;

BEGIN
    OPEN c_student;

    LOOP
        FETCH c_student INTO s_id, s_name, s_dept;

        EXIT WHEN c_student%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE(
            s_id || ' ' || s_name || ' ' || s_dept
        );
    END LOOP;

    CLOSE c_student;
END;
/
```

## Execute

```sql
EXEC Show_Students;
```

---

# 2. Count Students Department-wise Using Cursor

```sql
CREATE OR REPLACE PROCEDURE Count_Students
AS
    CURSOR c_dept IS
        SELECT Dept_ID, COUNT(*) Total
        FROM Student
        GROUP BY Dept_ID;

    d_id INT;
    total INT;

BEGIN
    OPEN c_dept;

    LOOP
        FETCH c_dept INTO d_id, total;

        EXIT WHEN c_dept%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE(
            'Department: ' || d_id ||
            ' Total Students: ' || total
        );
    END LOOP;

    CLOSE c_dept;
END;
/
```

## Execute

```sql
EXEC Count_Students;
```

---

# 3. Update Marks Less Than 40

```sql
CREATE OR REPLACE PROCEDURE Update_Marks
AS
BEGIN
    UPDATE Enrollment
    SET Marks = Marks + 10
    WHERE Marks < 40;
END;
/
```

## Execute

```sql
EXEC Update_Marks;
```

---

# 4. Function to Find Highest Marks

```sql
CREATE OR REPLACE FUNCTION Highest_Marks(
    c_id INT
)
RETURN INT
IS
    highest INT;
BEGIN
    SELECT MAX(Marks)
    INTO highest
    FROM Enrollment
    WHERE Course_ID = c_id;

    RETURN highest;
END;
/
```

## Execute

```sql
SELECT Highest_Marks(201) FROM dual;
```

---

# 5. Display Student Names Along with Courses

```sql
SELECT s.Name, c.Course_Name
FROM Student s
JOIN Enrollment e
ON s.Student_ID = e.Student_ID
JOIN Course c
ON e.Course_ID = c.Course_ID;
```

---

# 6. Function to Calculate Average Marks

```sql
CREATE OR REPLACE FUNCTION Average_Marks
RETURN NUMBER
IS
    avg_marks NUMBER;
BEGIN
    SELECT AVG(Marks)
    INTO avg_marks
    FROM Enrollment;

    RETURN avg_marks;
END;
/
```

## Execute

```sql
SELECT Average_Marks FROM dual;
```

---

# 7. Delete Students with Marks Below 30

```sql
CREATE OR REPLACE PROCEDURE Delete_Students
AS
BEGIN
    DELETE FROM Student
    WHERE Student_ID IN (
        SELECT Student_ID
        FROM Enrollment
        WHERE Marks < 30
    );
END;
/
```

## Execute

```sql
EXEC Delete_Students;
```

---

# 8. Generate Grade Report Using Cursor

```sql
CREATE OR REPLACE PROCEDURE Grade_Report
AS
    CURSOR c_grade IS
        SELECT Student_ID, Marks
        FROM Enrollment;

    s_id INT;
    m INT;
    grade CHAR(1);

BEGIN
    OPEN c_grade;

    LOOP
        FETCH c_grade INTO s_id, m;

        EXIT WHEN c_grade%NOTFOUND;

        IF m >= 80 THEN
            grade := 'A';

        ELSIF m >= 60 THEN
            grade := 'B';

        ELSE
            grade := 'C';

        END IF;

        DBMS_OUTPUT.PUT_LINE(
            'Student: ' || s_id ||
            ' Grade: ' || grade
        );
    END LOOP;

    CLOSE c_grade;
END;
/
```

## Execute

```sql
EXEC Grade_Report;
```

---

# 9. Count Departments Having Budget Greater Than Given Value

```sql
CREATE OR REPLACE FUNCTION Count_Department(
    min_budget NUMBER
)
RETURN INT
IS
    total INT;
BEGIN
    SELECT COUNT(*)
    INTO total
    FROM Department
    WHERE Budget > min_budget;

    RETURN total;
END;
/
```

## Execute

```sql
SELECT Count_Department(400000) FROM dual;
```

---

# 10. Find Topper in Each Course Using Cursor

```sql
CREATE OR REPLACE PROCEDURE Course_Topper
AS
    CURSOR c_topper IS
        SELECT Course_ID,
               MAX(Marks)
        FROM Enrollment
        GROUP BY Course_ID;

    c_id INT;
    top_marks INT;

BEGIN
    OPEN c_topper;

    LOOP
        FETCH c_topper INTO c_id, top_marks;

        EXIT WHEN c_topper%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE(
            'Course: ' || c_id ||
            ' Top Marks: ' || top_marks
        );
    END LOOP;

    CLOSE c_topper;
END;
/
```

## Execute

```sql
EXEC Course_Topper;
```

---

# Concepts Used

- CREATE PROCEDURE
- CREATE FUNCTION
- CURSOR
- LOOP Statements
- FETCH Statement
- IN Parameters
- Aggregate Functions
- Conditional Statements

---

# Simple Understanding

| Concept | Meaning |
|---|---|
| Procedure | Performs a task |
| Function | Returns a value |
| Cursor | Reads rows one by one |
| FETCH | Gets next row |
| LOOP | Repeats statements |
| DBMS_OUTPUT.PUT_LINE | Prints output |

---

# Conclusion

Successfully performed Stored Procedure and Function operations using Cursors for fetching, updating, deleting, and generating reports from the Student Database System.
