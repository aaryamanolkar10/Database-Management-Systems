# Subqueries in SQL

## Aim
To perform various subquery operations using the Library Management System database.

---

# Tables Used

## Books
- book_id
- title
- author
- price

## Members
- member_id
- name
- city

## Issued_Books
- issue_id
- book_id
- member_id
- issue_date
- return_date

---

# Step 1: Create Tables

```sql
CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(50),
    author VARCHAR(50),
    price DECIMAL(10,2)
);

CREATE TABLE Members (
    member_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);

CREATE TABLE Issued_Books (
    issue_id INT PRIMARY KEY,
    book_id INT,
    member_id INT,
    issue_date DATE,
    return_date DATE,
    FOREIGN KEY (book_id) REFERENCES Books(book_id),
    FOREIGN KEY (member_id) REFERENCES Members(member_id)
);
```

---

# Step 2: Insert Records

```sql
INSERT INTO Books VALUES (1, 'DBMS', 'Korth', 500);
INSERT INTO Books VALUES (2, 'Java', 'Herbert', 650);
INSERT INTO Books VALUES (3, 'Python', 'Guido', 450);
INSERT INTO Books VALUES (4, 'C Programming', 'Dennis', 700);

INSERT INTO Members VALUES (101, 'Aarya', 'Pune');
INSERT INTO Members VALUES (102, 'Rahul', 'Mumbai');
INSERT INTO Members VALUES (103, 'Sneha', 'Nashik');

INSERT INTO Issued_Books VALUES (1, 1, 101, '2026-01-10', '2026-01-20');
INSERT INTO Issued_Books VALUES (2, 2, 102, '2026-02-05', '2026-02-15');
INSERT INTO Issued_Books VALUES (3, 1, 103, '2026-03-01', '2026-03-10');
```

---

# 1. Find Books Costing More Than Average Price

```sql
SELECT *
FROM Books
WHERE price > (
    SELECT AVG(price)
    FROM Books
);
```

---

# 2. Display Members Who Have Issued At Least One Book

```sql
SELECT *
FROM Members
WHERE member_id IN (
    SELECT member_id
    FROM Issued_Books
);
```

---

# 3. Find Books That Have Never Been Issued

```sql
SELECT *
FROM Books
WHERE book_id NOT IN (
    SELECT book_id
    FROM Issued_Books
);
```

---

# 4. Display Members Who Issued Books After a Specific Member

```sql
SELECT *
FROM Members
WHERE member_id IN (
    SELECT member_id
    FROM Issued_Books
    WHERE issue_date > (
        SELECT issue_date
        FROM Issued_Books
        WHERE member_id = 101
    )
);
```

---

# 5. Find the Most Expensive Book

```sql
SELECT *
FROM Books
WHERE price = (
    SELECT MAX(price)
    FROM Books
);
```

---

# 6. Display Members Who Have Not Issued Any Books

```sql
SELECT *
FROM Members
WHERE member_id NOT IN (
    SELECT member_id
    FROM Issued_Books
);
```

---

# 7. Find Books Issued by a Specific Member

```sql
SELECT title
FROM Books
WHERE book_id IN (
    SELECT book_id
    FROM Issued_Books
    WHERE member_id = 101
);
```

---

# 8. Display Members Who Issued More Books Than Average Issued Count

```sql
SELECT member_id, COUNT(book_id) AS Total_Books
FROM Issued_Books
GROUP BY member_id
HAVING COUNT(book_id) > (
    SELECT AVG(Book_Count)
    FROM (
        SELECT COUNT(book_id) AS Book_Count
        FROM Issued_Books
        GROUP BY member_id
    )
);
```

---

# 9. Find the Latest Issued Book

```sql
SELECT *
FROM Books
WHERE book_id = (
    SELECT book_id
    FROM Issued_Books
    WHERE issue_date = (
        SELECT MAX(issue_date)
        FROM Issued_Books
    )
);
```

---

# 10. Display Books Priced Higher Than Books Written by a Specific Author

```sql
SELECT *
FROM Books
WHERE price > ANY (
    SELECT price
    FROM Books
    WHERE author = 'Guido'
);
```

---

# Concepts Used

- Single Row Subquery
- Multiple Row Subquery
- Nested Subquery
- Correlated Subquery
- IN Operator
- NOT IN Operator
- ANY Operator
- Aggregate Functions with Subqueries

---

# Conclusion

Successfully performed various subquery operations in SQL to retrieve, compare, and filter records using nested queries and aggregate functions.
