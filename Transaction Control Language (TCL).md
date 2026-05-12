# Transaction Control Language (TCL)

## Aim
To perform Transaction Control Language (TCL) operations on the Students table using SQL commands.

---

# Create Students Table

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR2(50),
    marks NUMBER(5,2)
);
```

---

# Insert Records and COMMIT Changes

```sql
INSERT INTO Students VALUES (1, 'Amit', 78);

INSERT INTO Students VALUES (2, 'Neha', 65);

COMMIT;
```

---

# Verify Inserted Records

```sql
SELECT * FROM Students;
```

---

# Insert Records and ROLLBACK Transaction

```sql
INSERT INTO Students VALUES (3, 'Rahul', 55);

INSERT INTO Students VALUES (4, 'Sneha', 72);

ROLLBACK;
```

---

# Verify ROLLBACK

```sql
SELECT * FROM Students;
```

Records with student_id 3 and 4 will not be displayed.

---

# Create SAVEPOINT

```sql
INSERT INTO Students VALUES (5, 'Karan', 81);

SAVEPOINT sp1;
```

---

# Perform More Changes

```sql
INSERT INTO Students VALUES (6, 'Priya', 69);

UPDATE Students
SET marks = 90
WHERE student_id = 5;
```

---

# Rollback to SAVEPOINT

```sql
ROLLBACK TO sp1;
```

This removes changes made after SAVEPOINT `sp1`.

---

# Verify SAVEPOINT Rollback

```sql
SELECT * FROM Students;
```

Student 6 will not exist and marks of student 5 will remain unchanged.

---

# Perform UPDATE and DELETE in Single Transaction

```sql
UPDATE Students
SET marks = 85
WHERE student_id = 1;

DELETE FROM Students
WHERE student_id = 2;
```

---

# Commit Final Changes

```sql
COMMIT;
```

---

# Verify Final Table

```sql
SELECT * FROM Students;
```

---

# Operations Performed

| Operation | Purpose |
|---|---|
| COMMIT | Saves transaction permanently |
| ROLLBACK | Cancels uncommitted transaction |
| SAVEPOINT | Creates a point within transaction |
| ROLLBACK TO SAVEPOINT | Returns to a specific savepoint |
| Transaction Management | Controls database transactions |

---

# Conclusion

Successfully performed TCL operations including COMMIT, ROLLBACK, SAVEPOINT, and transaction management using SQL commands.