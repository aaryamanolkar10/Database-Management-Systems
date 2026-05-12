# JOIN Operations in SQL

## Aim
To perform different types of JOIN operations in SQL for retrieving related data from multiple tables.

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

# Types of JOINs

| JOIN Type | Description |
|---|---|
| INNER JOIN | Returns only matching records from both tables |
| LEFT OUTER JOIN | Returns all records from left table and matching records from right table |
| RIGHT OUTER JOIN | Returns all records from right table and matching records from left table |
| FULL OUTER JOIN | Returns all records from both tables |
| SELF JOIN | Joins a table with itself |

---

# SQL Queries

## 1. INNER JOIN

```sql
SELECT s.Name, d.Dept_Name
FROM Student s
INNER JOIN Department d
ON s.Dept_ID = d.Dept_ID;
```

### Output
Displays student names with their department names.

---

## 2. LEFT OUTER JOIN

```sql
SELECT s.Name, c.Course_Name
FROM Student s
LEFT JOIN Enrollment e
ON s.Student_ID = e.Student_ID
LEFT JOIN Course c
ON e.Course_ID = c.Course_ID;
```

### Output
Displays all students including those not enrolled in courses.

---

## 3. RIGHT OUTER JOIN

```sql
SELECT s.Name, d.Dept_Name
FROM Student s
RIGHT JOIN Department d
ON s.Dept_ID = d.Dept_ID;
```

### Output
Displays all departments including departments without students.

---

## 4. FULL OUTER JOIN

```sql
SELECT s.Name, d.Dept_Name
FROM Student s
FULL OUTER JOIN Department d
ON s.Dept_ID = d.Dept_ID;
```

### Output
Displays all students and departments whether matching exists or not.

---

## 5. SELF JOIN

```sql
SELECT A.Name AS Student1, B.Name AS Student2
FROM Student A
JOIN Student B
ON A.Dept_ID = B.Dept_ID
WHERE A.Student_ID <> B.Student_ID;
```

### Output
Displays students belonging to the same department.

---

# Aggregate Function with JOIN

```sql
SELECT c.Course_Name, COUNT(e.Student_ID) AS Total_Students
FROM Course c
LEFT JOIN Enrollment e
ON c.Course_ID = e.Course_ID
GROUP BY c.Course_Name;
```

### Output
Displays total number of students enrolled in each course.

---

# Concepts Used

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- SELF JOIN
- GROUP BY
- COUNT()
- Aggregate Functions

---

# Conclusion

Successfully performed different JOIN operations in SQL to retrieve related data from multiple tables and generate summary reports.
