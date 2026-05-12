# Data Control Language (DCL)

## Aim
To perform Data Control Language (DCL) operations for user access management using SQL commands.

---

# Step 1: Create a New User

```sql
CREATE USER student_user
IDENTIFIED BY student123;
```

---

# Step 2: Grant CONNECT Privilege

```sql
GRANT CONNECT TO student_user;
```

---

# Step 3: Create Students Table

```sql
CREATE TABLE Students (
    student_id INT,
    name VARCHAR2(50),
    marks NUMBER(5,2)
);
```

---

# Step 4: Grant SELECT Privilege on Students Table

```sql
GRANT SELECT
ON Students
TO student_user;
```

---

# Step 5: Grant UPDATE Privilege

```sql
GRANT UPDATE
ON Students
TO student_user;
```

---

# Step 6: Test SELECT Permission

Login as new user:

```sql
CONNECT student_user/student123;
```

Run:

```sql
SELECT * FROM system.Students;
```

---

# Step 7: Test UPDATE Permission

```sql
UPDATE system.Students
SET marks = 90
WHERE student_id = 1;
```

---

# Step 8: Revoke UPDATE Privilege

Login as SYSTEM user:

```sql
CONNECT system/password;

REVOKE UPDATE
ON Students
FROM student_user;
```

---

# Step 9: Test UPDATE After REVOKE

Login again as `student_user` and run:

```sql
UPDATE system.Students
SET marks = 95
WHERE student_id = 1;
```

Expected Error:

```text
ORA-01031: insufficient privileges
```

---

# Step 10: Create Role

```sql
CREATE ROLE student_role;
```

---

# Step 11: Assign Permissions to Role

```sql
GRANT SELECT, INSERT
ON Students
TO student_role;
```

---

# Step 12: Assign Role to User

```sql
GRANT student_role
TO student_user;
```

---

# Step 13: Test INSERT Using Role

Login as `student_user`:

```sql
INSERT INTO system.Students
VALUES (1, 'Amit', 78);
```

---

# Optional Verification Queries

## View Users

```sql
SELECT username
FROM all_users;
```

---

## View Table Privileges

```sql
SELECT *
FROM user_tab_privs;
```

---

## View Roles

```sql
SELECT *
FROM user_role_privs;
```

---

# Operations Performed

| Operation | Purpose |
|---|---|
| CREATE USER | Creates a new database user |
| GRANT | Gives privileges to user or role |
| REVOKE | Removes privileges |
| CREATE ROLE | Creates a group of privileges |
| Role Assignment | Assigns role to user |

---

# Conclusion

Successfully performed DCL operations including user creation, granting privileges, revoking permissions, role creation, and role assignment using SQL commands.