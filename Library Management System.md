# Library Management System - DBMS Practical

## Problem Statement
Create a Library Management System database.

---

# Objectives
- Create tables using SQL
- Apply Primary Key and Foreign Key constraints
- Apply CHECK constraint
- Perform ALTER, RENAME, TRUNCATE, and DROP operations

---

# E-R Diagram

```text
BOOK
-----
Book_ID (PK)
Title
Price
Book_Category

        |
        |  (Referenced by)
        |

ISSUE
-----
Issue_ID (PK)
Book_ID (FK)
Member_ID (FK)

        |
        |  (Referenced by)
        |

MEMBER
------
Member_ID (PK)
Member_Name
```

---

# SQL Queries

## Step 1: Drop Existing Tables

```sql
DROP TABLE Employee CASCADE CONSTRAINTS;
DROP TABLE Department CASCADE CONSTRAINTS;
```

---

# Step 2: Create Book Table

```sql
CREATE TABLE Book (
    Book_ID INT PRIMARY KEY,
    Title VARCHAR(100),
    Price DECIMAL(10,2) CHECK (Price > 0)
);
```

---

# Step 3: Create Member Table

```sql
CREATE TABLE Member (
    Member_ID INT PRIMARY KEY,
    Member_Name VARCHAR(100)
);
```

---

# Step 4: Create Issue Table

```sql
CREATE TABLE Issue (
    Issue_ID INT PRIMARY KEY,
    Book_ID INT,
    Member_ID INT,

    CONSTRAINT fk_book
        FOREIGN KEY (Book_ID)
        REFERENCES Book(Book_ID),

    CONSTRAINT fk_member
        FOREIGN KEY (Member_ID)
        REFERENCES Member(Member_ID)
);
```

---

# Step 5: Insert Sample Data

## Insert into Book Table

```sql
INSERT INTO Book VALUES (101, 'Database Management System', 550);
INSERT INTO Book VALUES (102, 'Operating System', 650);
INSERT INTO Book VALUES (103, 'Computer Networks', 700);
```

## Insert into Member Table

```sql
INSERT INTO Member VALUES (1, 'Aarya');
INSERT INTO Member VALUES (2, 'Rahul');
INSERT INTO Member VALUES (3, 'Sneha');
```

## Insert into Issue Table

```sql
INSERT INTO Issue VALUES (1001, 101, 1);
INSERT INTO Issue VALUES (1002, 102, 2);
INSERT INTO Issue VALUES (1003, 103, 3);
```

---

# Step 6: Add New Column

```sql
ALTER TABLE Book
ADD Book_Category VARCHAR(50);
```

---

# Step 7: Rename Table

```sql
RENAME Member TO Library_Member;
```

---

# Step 8: Truncate Issue Table

```sql
TRUNCATE TABLE Issue;
```

---

# View Table Structure

```sql
DESC Book;
DESC Library_Member;
DESC Issue;
```

---

# View Data

```sql
SELECT * FROM Book;
SELECT * FROM Library_Member;
SELECT * FROM Issue;
```

---

# Concepts Learned

- Primary Key
- Foreign Key
- CHECK Constraint
- ALTER TABLE
- RENAME TABLE
- TRUNCATE TABLE
- DROP TABLE
- DESC Command

---

# Difference Between Important Commands

| Command | Purpose |
|---|---|
| DESC | Shows table structure |
| SELECT * | Shows table data |
| TRUNCATE | Deletes all rows only |
| DROP | Deletes complete table |

---

# Result
Successfully created and managed the Library Management System database using SQL queries and constraints.