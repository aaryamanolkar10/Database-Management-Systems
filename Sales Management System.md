# Sales Management System

## Aim
To develop a Sales Management System database using SQL with constraints and aggregate functions.

---

# E-R Diagram

```text
+-------------------+
|       SALES       |
+-------------------+
| sale_id (PK)      |
| sale_date         |
| amount            |
+-------------------+
```

---

# Create Sales Table

```sql
CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    sale_date DATE NOT NULL,
    amount NUMBER(10,2),

    CONSTRAINT chk_amount
    CHECK (amount > 0)
);
```

---

# Insert Sample Records

```sql
INSERT INTO Sales VALUES (101, '01-JAN-2026', 5000);

INSERT INTO Sales VALUES (102, '03-JAN-2026', 7000);

INSERT INTO Sales VALUES (103, '05-JAN-2026', 3000);

INSERT INTO Sales VALUES (104, '08-JAN-2026', 9000);

INSERT INTO Sales VALUES (105, '10-JAN-2026', 4500);
```

---

# Display Table Data

```sql
SELECT * FROM Sales;
```

---

# View Table Structure

```sql
DESC Sales;
```

---

# Aggregate Function Operations

## 1. Calculate Total Sales Amount

```sql
SELECT SUM(amount) AS Total_Sales
FROM Sales;
```

---

## 2. Display Average Sales Amount

```sql
SELECT AVG(amount) AS Average_Sales
FROM Sales;
```

---

## 3. Find Maximum Sales Amount

```sql
SELECT MAX(amount) AS Maximum_Sales
FROM Sales;
```

---

## 4. Find Minimum Sales Amount

```sql
SELECT MIN(amount) AS Minimum_Sales
FROM Sales;
```

---

## 5. Count Total Sales Transactions

```sql
SELECT COUNT(*) AS Total_Transactions
FROM Sales;
```

---

# Conclusion

Successfully created a Sales Management System database using SQL with constraints and aggregate functions like SUM, AVG, MAX, MIN, and COUNT.