# Department and Employee Management Database

## Aim
Develop a database for Department and Employee Management using SQL*Plus.

---

# Step 1: Create Department Table

```sql
CREATE TABLE Department(
    Department_ID NUMBER PRIMARY KEY,
    Department_Name VARCHAR2(50) NOT NULL
);
```

---

# Step 2: Create Employee Table

```sql
CREATE TABLE Employee(
    Employee_ID NUMBER PRIMARY KEY,
    Employee_Name VARCHAR2(50) NOT NULL,
    Salary NUMBER(10,2),
    Department_ID NUMBER,

    CONSTRAINT chk_salary
    CHECK (Salary > 10000),

    CONSTRAINT fk_department
    FOREIGN KEY (Department_ID)
    REFERENCES Department(Department_ID)
);
```

---

# Step 3: Insert Records into Department Table

```sql
INSERT INTO Department VALUES (101, 'HR');

INSERT INTO Department VALUES (102, 'Finance');

INSERT INTO Department VALUES (103, 'IT');
```

---

# Step 4: Display Department Table

```sql
SELECT * FROM Department;
```

## Output

| Department_ID | Department_Name |
|----------------|----------------|
| 101 | HR |
| 102 | Finance |
| 103 | IT |

---

# Step 5: Insert Records into Employee Table

```sql
INSERT INTO Employee VALUES (1, 'Aarya', 25000, 101);

INSERT INTO Employee VALUES (2, 'Rohit', 30000, 102);

INSERT INTO Employee VALUES (3, 'Sneha', 45000, 103);
```

---

# Step 6: Display Employee Table

```sql
SELECT * FROM Employee;
```

## Output

| Employee_ID | Employee_Name | Salary | Department_ID |
|-------------|---------------|---------|----------------|
| 1 | Aarya | 25000 | 101 |
| 2 | Rohit | 30000 | 102 |
| 3 | Sneha | 45000 | 103 |

---

# Step 7: Modify Employee Table

Add Contact_Number column.

```sql
ALTER TABLE Employee
ADD Contact_Number VARCHAR2(15);
```

---

# Step 8: Update Contact Number

```sql
UPDATE Employee
SET Contact_Number = '123456'
WHERE Employee_ID = 1;
```

---

# Step 9: Display Updated Employee Table

```sql
SELECT * FROM Employee;
```

## Output

| Employee_ID | Employee_Name | Salary | Department_ID | Contact_Number |
|-------------|---------------|---------|----------------|----------------|
| 1 | Aarya | 25000 | 101 | 123456 |
| 2 | Rohit | 30000 | 102 | NULL |
| 3 | Sneha | 45000 | 103 | NULL |

---

# Step 10: Commit Changes

```sql
COMMIT;
```

---

# Constraints Used

- `PRIMARY KEY` on Employee_ID
- `FOREIGN KEY` on Department_ID
- `CHECK` constraint on Salary > 10000
- `NOT NULL` constraint on Employee_Name and Department_Name

---

# Conclusion

Successfully created and managed the Department and Employee database using SQL*Plus with constraints and table modification operations.