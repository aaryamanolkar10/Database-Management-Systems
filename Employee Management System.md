# Employee Management System

## Aim
To develop an Employee Management System database using SQL with constraints and aggregate functions.

---

# E-R Diagram

```text
+-------------------+
|    DEPARTMENT     |
+-------------------+
| dept_id (PK)      |
| dept_name         |
+-------------------+
          |
          | 1
          |
          | M
+-------------------+
|     EMPLOYEE      |
+-------------------+
| emp_id (PK)       |
| name              |
| dept_id (FK)      |
| job               |
| salary            |
+-------------------+
```

---

# Create Department Table

```sql
CREATE TABLE Department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR2(50) NOT NULL
);
```

---

# Create Employee Table

```sql
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    name VARCHAR2(50) NOT NULL,
    dept_id INT,
    job VARCHAR2(50),
    salary NUMBER(10,2),

    CONSTRAINT fk_department
    FOREIGN KEY (dept_id)
    REFERENCES Department(dept_id),

    CONSTRAINT chk_salary
    CHECK (salary > 0)
);
```

---

# Insert Sample Records

## Insert into Department

```sql
INSERT INTO Department VALUES (1, 'HR');
INSERT INTO Department VALUES (2, 'IT');
INSERT INTO Department VALUES (3, 'Finance');
```

## Insert into Employee

```sql
INSERT INTO Employee VALUES (101, 'Amit', 1, 'Manager', 50000);

INSERT INTO Employee VALUES (102, 'Rahul', 2, 'Developer', 60000);

INSERT INTO Employee VALUES (103, 'Sneha', 2, 'Tester', 45000);

INSERT INTO Employee VALUES (104, 'Priya', 3, 'Accountant', 55000);

INSERT INTO Employee VALUES (105, 'Karan', 1, 'Executive', 40000);
```

---

# Display Tables

```sql
SELECT * FROM Department;

SELECT * FROM Employee;
```

---

# Aggregate Function Operations

## 1. Display Maximum Employee Salary

```sql
SELECT MAX(salary) AS Maximum_Salary
FROM Employee;
```

---

## 2. Display Minimum Employee Salary

```sql
SELECT MIN(salary) AS Minimum_Salary
FROM Employee;
```

---

## 3. Calculate Average Salary Department-wise

```sql
SELECT dept_id,
       AVG(salary) AS Average_Salary
FROM Employee
GROUP BY dept_id;
```

---

## 4. Count Total Employees in Each Department

```sql
SELECT dept_id,
       COUNT(*) AS Total_Employees
FROM Employee
GROUP BY dept_id;
```

---

## 5. Calculate Total Salary Paid Department-wise

```sql
SELECT dept_id,
       SUM(salary) AS Total_Salary
FROM Employee
GROUP BY dept_id;
```

---

# View Table Structure

```sql
DESC Department;

DESC Employee;
```

---

# Conclusion

Successfully created an Employee Management System database with primary key, foreign key, and check constraints. Performed aggregate operations such as MAX, MIN, AVG, COUNT, and SUM using SQL queries.