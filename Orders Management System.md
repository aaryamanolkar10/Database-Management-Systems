# Orders Management System

## Aim
To create an Orders Management System database using SQL with constraints and aggregate functions.

---

# E-R Diagram

```text
+-------------------+
|      ORDERS       |
+-------------------+
| order_id (PK)     |
| customer_id       |
| order_date        |
| amount            |
+-------------------+
```

---

# Create Orders Table

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE NOT NULL,
    amount NUMBER(10,2),

    CONSTRAINT chk_amount
    CHECK (amount > 0)
);
```

---

# Insert Sample Records

```sql
INSERT INTO Orders VALUES (101, 1, '01-JAN-2026', 5000);

INSERT INTO Orders VALUES (102, 2, '05-JAN-2026', 7000);

INSERT INTO Orders VALUES (103, 1, '10-JAN-2026', 3000);

INSERT INTO Orders VALUES (104, 3, '12-JAN-2026', 9000);

INSERT INTO Orders VALUES (105, 2, '15-JAN-2026', 4000);
```

---

# Display Table Data

```sql
SELECT * FROM Orders;
```

---

# View Table Structure

```sql
DESC Orders;
```

---

# Aggregate Function Operations

## 1. Calculate Total Order Amount

```sql
SELECT SUM(amount) AS Total_Order_Amount
FROM Orders;
```

---

## 2. Display Average Order Amount

```sql
SELECT AVG(amount) AS Average_Order_Amount
FROM Orders;
```

---

## 3. Find Highest Order Amount

```sql
SELECT MAX(amount) AS Highest_Order_Amount
FROM Orders;
```

---

## 4. Find Lowest Order Amount

```sql
SELECT MIN(amount) AS Lowest_Order_Amount
FROM Orders;
```

---

## 5. Calculate Customer-wise Total Purchase Amount

```sql
SELECT customer_id,
       SUM(amount) AS Total_Purchase
FROM Orders
GROUP BY customer_id;
```

---

# Conclusion

Successfully created an Orders Management System database using SQL with constraints and aggregate functions such as SUM, AVG, MAX, MIN, and GROUP BY.