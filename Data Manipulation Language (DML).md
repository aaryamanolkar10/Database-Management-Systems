# Data Manipulation Language (DML)

## Aim
To perform DML operations, arithmetic operators, logical operators, set operators, pattern matching, and string functions using SQL queries on the Students table.

---

# Create Students Table

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR2(50),
    department VARCHAR2(30),
    city VARCHAR2(30),
    marks NUMBER(5,2)
);
```

---

# Insert Records

```sql
INSERT INTO Students VALUES (1, 'Amit', 'Computer', 'Pune', 78);

INSERT INTO Students VALUES (2, 'Akash', 'IT', 'Mumbai', 65);

INSERT INTO Students VALUES (3, 'Ramesh', 'EXTC', 'Pune', 55);

INSERT INTO Students VALUES (4, 'Ashit', 'Computer', 'Nashik', 32);

INSERT INTO Students VALUES (5, 'Neha', 'Civil', 'Pune', 48);
```

---

# DML Operations

## 1. Insert a New Student Record

```sql
INSERT INTO Students
VALUES (6, 'Ankit', 'IT', 'Pune', 72);
```

---

## 2. Update Marks of Computer Department Students

```sql
UPDATE Students
SET marks = marks + 5
WHERE department = 'Computer';
```

---

## 3. Delete Students Scoring Less Than 35

```sql
DELETE FROM Students
WHERE marks < 35;
```

---

## 4. Display Names Starting with 'A' in Uppercase

```sql
SELECT UPPER(name)
FROM Students
WHERE name LIKE 'A%';
```

---

## 5. Display Students from IT and Computer Departments using UNION

```sql
SELECT name, department
FROM Students
WHERE department = 'IT'

UNION

SELECT name, department
FROM Students
WHERE department = 'Computer';
```

---

# Arithmetic Operators

## 1. Add 10 Marks

```sql
SELECT name,
       marks + 10 AS Updated_Marks
FROM Students;
```

---

## 2. Average Marks with Bonus

```sql
SELECT AVG(marks + 5) AS Average_Marks
FROM Students;
```

---

## 3. Display Percentage Marks

```sql
SELECT name,
       (marks / 100) * 100 AS Percentage
FROM Students;
```

---

## 4. Reduce Marks by 5

```sql
SELECT name,
       marks - 5 AS Penalized_Marks
FROM Students;
```

---

## 5. Multiply Marks for Grading Scale

```sql
SELECT name,
       marks * 2 AS Grading_Scale
FROM Students;
```

---

# Logical Operators

## 1. Students with Marks Greater Than 70 from Computer Department

```sql
SELECT *
FROM Students
WHERE marks > 70
AND department = 'Computer';
```

---

## 2. Students from IT or EXTC Department

```sql
SELECT *
FROM Students
WHERE department = 'IT'
OR department = 'EXTC';
```

---

## 3. Students Not Belonging to Civil Department

```sql
SELECT *
FROM Students
WHERE NOT department = 'Civil';
```

---

## 4. Students with Marks Between 50 and 80

```sql
SELECT *
FROM Students
WHERE marks BETWEEN 50 AND 80;
```

---

## 5. Students from Pune Scoring Less Than 60

```sql
SELECT *
FROM Students
WHERE city = 'Pune'
AND marks < 60;
```

---

# Set Operators

## 1. UNION

```sql
SELECT name FROM Students
WHERE department = 'IT'

UNION

SELECT name FROM Students
WHERE department = 'Computer';
```

---

## 2. UNION ALL

```sql
SELECT name FROM Students
WHERE department = 'IT'

UNION ALL

SELECT name FROM Students
WHERE department = 'Computer';
```

---

## 3. INTERSECT

```sql
SELECT name FROM Students
WHERE department = 'IT'

INTERSECT

SELECT name FROM Students
WHERE marks > 60;
```

---

## 4. MINUS (EXCEPT in Oracle)

```sql
SELECT name FROM Students
WHERE department = 'IT'

MINUS

SELECT name FROM Students
WHERE department = 'Computer';
```

---

## 5. Multiple UNION Operations

```sql
SELECT name FROM Students
WHERE department = 'IT'

UNION

SELECT name FROM Students
WHERE department = 'Computer'

UNION

SELECT name FROM Students
WHERE department = 'EXTC';
```

---

# Pattern Matching

## 1. Names Starting with 'A'

```sql
SELECT *
FROM Students
WHERE name LIKE 'A%';
```

---

## 2. Names Ending with 'a'

```sql
SELECT *
FROM Students
WHERE name LIKE '%a';
```

---

## 3. Names Containing 'sh'

```sql
SELECT *
FROM Students
WHERE name LIKE '%sh%';
```

---

## 4. Names Having Exactly 5 Characters

```sql
SELECT *
FROM Students
WHERE name LIKE '_____';
```

---

## 5. Names Starting with 'A' and Ending with 't'

```sql
SELECT *
FROM Students
WHERE name LIKE 'A%t';
```

---

# String Functions

## 1. Convert Names to Uppercase

```sql
SELECT UPPER(name)
FROM Students;
```

---

## 2. Convert Names to Lowercase

```sql
SELECT LOWER(name)
FROM Students;
```

---

## 3. Display Length of Names

```sql
SELECT name,
       LENGTH(name) AS Name_Length
FROM Students;
```

---

## 4. Concatenate Name and Department

```sql
SELECT CONCAT(name, department) AS Student_Info
FROM Students;
```

---

## 5. Extract First 3 Characters

```sql
SELECT SUBSTR(name, 1, 3) AS Short_Name
FROM Students;
```

---

# Difference Between UNION and UNION ALL

| UNION | UNION ALL |
|---|---|
| Removes duplicate records | Displays duplicate records |
| Returns only unique values | Returns all values |
| Slower because duplicates are checked | Faster because no duplicate checking |

---

# Conclusion

Successfully performed DML operations, arithmetic operations, logical operations, set operations, pattern matching, and string functions using SQL queries on the Students table.