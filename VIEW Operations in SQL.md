# VIEW Operations in SQL

## Aim
To perform various VIEW operations in SQL for simplifying data access and managing virtual tables.

---

# Tables Used

## Student
- Student_ID
- Name
- Dept_ID

## Department
- Dept_ID
- Dept_Name

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
    Dept_Name VARCHAR(50)
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
INSERT INTO Department VALUES (1, 'Computer');
INSERT INTO Department VALUES (2, 'Mechanical');

INSERT INTO Student VALUES (101, 'Aarya', 1);
INSERT INTO Student VALUES (102, 'Rahul', 2);

INSERT INTO Course VALUES (201, 'DBMS');
INSERT INTO Course VALUES (202, 'Java');

INSERT INTO Enrollment VALUES (101, 201, 85);
INSERT INTO Enrollment VALUES (102, 202, 78);

INSERT INTO Faculty VALUES (1, 'Dr. Sharma', 1);
INSERT INTO Faculty VALUES (2, 'Prof. Mehta', 2);
```

---

# 1. Create View for Student and Department Names

```sql
CREATE VIEW Student_Department_View AS
SELECT s.Name, d.Dept_Name
FROM Student s
JOIN Department d
ON s.Dept_ID = d.Dept_ID;
```

## Display View

```sql
SELECT * FROM Student_Department_View;
```

---

# 2. Create View on Student Table

```sql
CREATE VIEW Student_View AS
SELECT * FROM Student;
```

---

# 3. Insert Records Through View

```sql
INSERT INTO Student_View
VALUES (103, 'Sneha', 1);
```

## Verify

```sql
SELECT * FROM Student;
```

---

# 4. Create Conditional View

```sql
CREATE VIEW Computer_Students AS
SELECT *
FROM Student
WHERE Dept_ID = 1;
```

## Display Conditional View

```sql
SELECT * FROM Computer_Students;
```

---

# 5. Update Records Through View

```sql
UPDATE Student_View
SET Name = 'Priya'
WHERE Student_ID = 102;
```

## Verify Update

```sql
SELECT * FROM Student;
```

---

# 6. Create Join View

```sql
CREATE VIEW Student_Course_View AS
SELECT s.Name, c.Course_Name, e.Marks
FROM Student s
JOIN Enrollment e
ON s.Student_ID = e.Student_ID
JOIN Course c
ON e.Course_ID = c.Course_ID;
```

## Display Join View

```sql
SELECT * FROM Student_Course_View;
```

---

# 7. Attempt Insertion into Join View

```sql
INSERT INTO Student_Course_View
VALUES ('Karan', 'Python', 88);
```

## Result
Insertion may fail because JOIN views are generally not updatable.

---

# 8. Delete Records Through View

```sql
DELETE FROM Student_View
WHERE Student_ID = 103;
```

## Verify Delete

```sql
SELECT * FROM Student;
```

---

# 9. Create View with CHECK OPTION

```sql
CREATE VIEW CS_Students AS
SELECT *
FROM Student
WHERE Dept_ID = 1
WITH CHECK OPTION;
```

---

# 10. Attempt Update Violating CHECK OPTION

```sql
UPDATE CS_Students
SET Dept_ID = 2
WHERE Student_ID = 101;
```

## Result
Update will fail because it violates the CHECK OPTION condition.

---

# 11. Drop View

```sql
DROP VIEW Student_Department_View;
```

---

# Concepts Used

- CREATE VIEW
- SELECT from VIEW
- INSERT through VIEW
- UPDATE through VIEW
- DELETE through VIEW
- JOIN VIEW
- CHECK OPTION
- DROP VIEW

---

# Conclusion

Successfully performed various VIEW operations in SQL including creating, updating, deleting, and managing virtual tables using views.
