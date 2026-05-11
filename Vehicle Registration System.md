# Vehicle Registration System

A SQL-based Vehicle Registration System demonstrating table creation, constraints, data insertion, table alteration, and deletion operations.

---

## Problem Statement

Create a Vehicle Registration System database.

### Tasks
1. Draw the E-R Diagram  
2. Create an Owner table with:
   - Owner_ID
   - Owner_Name
3. Create a Vehicle table with:
   - Registration_Number
   - Vehicle_Type
   - Year
   - Owner_ID

### Apply Constraints
- Registration_Number as PRIMARY KEY
- Owner_ID as FOREIGN KEY
- Vehicle year must be greater than 2000

### Perform the Following Operations
1. Insert sample data
2. Alter the Vehicle table to add Insurance_Number
3. Drop the Vehicle table

---

# E-R Diagram

```text
+------------------+          +----------------------+
|      Owner       |          |       Vehicle        |
+------------------+          +----------------------+
| Owner_ID (PK)    |<-------> | Registration_Number  |
| Owner_Name       |          | Vehicle_Type         |
+------------------+          | Year                 |
                              | Owner_ID (FK)        |
                              +----------------------+
```

---

# SQL Queries

## 1. Create Owner Table

```sql
CREATE TABLE Owner (
    Owner_ID INT PRIMARY KEY,
    Owner_Name VARCHAR2(50) NOT NULL
);
```

---

## 2. Create Vehicle Table

```sql
CREATE TABLE Vehicle (
    Registration_Number VARCHAR2(20) PRIMARY KEY,
    Vehicle_Type VARCHAR2(30),
    Year INT CHECK (Year > 2000),
    Owner_ID INT,

    CONSTRAINT fk_owner
    FOREIGN KEY (Owner_ID)
    REFERENCES Owner(Owner_ID)
);
```

---

## 3. Insert Sample Data

```sql
INSERT INTO Owner VALUES (1, 'Aarya');
INSERT INTO Owner VALUES (2, 'Rahul');
INSERT INTO Owner VALUES (3, 'Sneha');

INSERT INTO Vehicle
VALUES ('MH12AB1234', 'Car', 2021, 1);

INSERT INTO Vehicle
VALUES ('MH14XY5678', 'Bike', 2022, 2);

INSERT INTO Vehicle
VALUES ('MH01CD9090', 'Truck', 2023, 3);
```

---

## 4. Display Tables

```sql
SELECT * FROM Owner;

SELECT * FROM Vehicle;
```

---

## 5. Alter Vehicle Table

```sql
ALTER TABLE Vehicle
ADD Insurance_Number VARCHAR2(30);
```

---

## 6. Describe Vehicle Table

```sql
DESC Vehicle;
```

---

## 7. Drop Vehicle Table

```sql
DROP TABLE Vehicle;
```

---

# Constraints Used

- PRIMARY KEY
- FOREIGN KEY
- CHECK Constraint
- NOT NULL Constraint

---

# Technologies Used

- Oracle SQL
- SQL*Plus

---

# Learning Outcomes

- Understanding database relationships
- Applying SQL constraints
- Using ALTER and DROP commands
- Managing relational database tables