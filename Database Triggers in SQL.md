# Database Triggers in SQL

## Aim
To implement and test database triggers for maintaining data integrity and automating operations in the Banking Database System.

---

# What is a Trigger?

A Trigger is a block of SQL code that automatically executes when an INSERT, UPDATE, or DELETE operation occurs.

- BEFORE Trigger → runs before operation
- AFTER Trigger → runs after operation

---

# Tables Used

## Account
- acc_id
- name
- balance

## Withdrawal
- wid
- acc_id
- amount

## Deposit
- did
- acc_id
- amount

## Transactions
- tx_id
- acc_id
- type
- amount
- tx_date

## Transaction_Log
- log_id
- tx_id
- acc_id
- action
- amount
- log_date

## Balance_History
- acc_id
- old_balance
- new_balance
- change_date

## Account_Auto
- acc_no
- name
- balance

---

# Step 1: Create Tables

```sql
CREATE TABLE Account (
    acc_id INT PRIMARY KEY,
    name VARCHAR(50),
    balance DECIMAL(10,2)
);

CREATE TABLE Withdrawal (
    wid INT PRIMARY KEY,
    acc_id INT,
    amount DECIMAL(10,2)
);

CREATE TABLE Deposit (
    did INT PRIMARY KEY,
    acc_id INT,
    amount DECIMAL(10,2)
);

CREATE TABLE Transactions (
    tx_id INT PRIMARY KEY,
    acc_id INT,
    type VARCHAR(20),
    amount DECIMAL(10,2),
    tx_date DATE
);

CREATE TABLE Transaction_Log (
    log_id INT PRIMARY KEY,
    tx_id INT,
    acc_id INT,
    action VARCHAR(20),
    amount DECIMAL(10,2),
    log_date DATE
);

CREATE TABLE Balance_History (
    acc_id INT,
    old_balance DECIMAL(10,2),
    new_balance DECIMAL(10,2),
    change_date DATE
);

CREATE TABLE Account_Auto (
    acc_no INT PRIMARY KEY,
    name VARCHAR(50),
    balance DECIMAL(10,2)
);
```

---

# Step 2: Insert Sample Records

```sql
INSERT INTO Account VALUES (101, 'Aarya', 10000);
INSERT INTO Account VALUES (102, 'Rahul', 5000);
```

---

# 1. Prevent Account Balance Below Minimum

```sql
CREATE OR REPLACE TRIGGER Min_Balance_Trigger
BEFORE INSERT ON Withdrawal
FOR EACH ROW
DECLARE
    current_balance NUMBER;
BEGIN
    SELECT balance
    INTO current_balance
    FROM Account
    WHERE acc_id = :NEW.acc_id;

    IF current_balance - :NEW.amount < 1000 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'Minimum balance must be maintained'
        );
    END IF;
END;
/
```

---

# 2. Automatically Deduct Balance After Withdrawal

```sql
CREATE OR REPLACE TRIGGER Withdraw_Trigger
AFTER INSERT ON Withdrawal
FOR EACH ROW
BEGIN
    UPDATE Account
    SET balance = balance - :NEW.amount
    WHERE acc_id = :NEW.acc_id;
END;
/
```

---

# 3. Prevent Invalid or Negative Deposits

```sql
CREATE OR REPLACE TRIGGER Deposit_Validation
BEFORE INSERT ON Deposit
FOR EACH ROW
BEGIN
    IF :NEW.amount <= 0 THEN
        RAISE_APPLICATION_ERROR(
            -20002,
            'Invalid deposit amount'
        );
    END IF;
END;
/
```

---

# 4. Maintain Transaction Audit Log Automatically

```sql
CREATE OR REPLACE TRIGGER Transaction_Log_Trigger
AFTER INSERT ON Transactions
FOR EACH ROW
BEGIN
    INSERT INTO Transaction_Log
    VALUES (
        :NEW.tx_id,
        :NEW.tx_id,
        :NEW.acc_id,
        :NEW.type,
        :NEW.amount,
        SYSDATE
    );
END;
/
```

---

# 5. Prevent Deletion of Accounts Having Balance

```sql
CREATE OR REPLACE TRIGGER Prevent_Delete
BEFORE DELETE ON Account
FOR EACH ROW
BEGIN
    IF :OLD.balance > 0 THEN
        RAISE_APPLICATION_ERROR(
            -20003,
            'Cannot delete account with balance'
        );
    END IF;
END;
/
```

---

# 6. Generate Account Numbers Automatically

## Create Sequence

```sql
CREATE SEQUENCE acc_seq
START WITH 1001
INCREMENT BY 1;
```

## Trigger Using Sequence

```sql
CREATE OR REPLACE TRIGGER Auto_Account_No
BEFORE INSERT ON Account_Auto
FOR EACH ROW
BEGIN
    :NEW.acc_no := acc_seq.NEXTVAL;
END;
/
```

---

# 7. Enforce Minimum Deposit Amount Rule

```sql
CREATE OR REPLACE TRIGGER Min_Deposit
BEFORE INSERT ON Deposit
FOR EACH ROW
BEGIN
    IF :NEW.amount < 500 THEN
        RAISE_APPLICATION_ERROR(
            -20004,
            'Minimum deposit is 500'
        );
    END IF;
END;
/
```

---

# 8. Track Balance Changes Automatically

```sql
CREATE OR REPLACE TRIGGER Balance_History_Trigger
AFTER UPDATE OF balance ON Account
FOR EACH ROW
BEGIN
    INSERT INTO Balance_History
    VALUES (
        :OLD.acc_id,
        :OLD.balance,
        :NEW.balance,
        SYSDATE
    );
END;
/
```

---

# 9. Prevent Duplicate Account Holder Names

```sql
CREATE OR REPLACE TRIGGER Unique_Name_Trigger
BEFORE INSERT ON Account
FOR EACH ROW
DECLARE
    total NUMBER;
BEGIN
    SELECT COUNT(*)
    INTO total
    FROM Account
    WHERE name = :NEW.name;

    IF total > 0 THEN
        RAISE_APPLICATION_ERROR(
            -20005,
            'Duplicate account holder name'
        );
    END IF;
END;
/
```

---

# 10. Automatically Insert Transaction Timestamp

```sql
CREATE OR REPLACE TRIGGER Transaction_Time
BEFORE INSERT ON Transactions
FOR EACH ROW
BEGIN
    :NEW.tx_date := SYSDATE;
END;
/
```

---

# Step 3: Test Triggers

## Test Withdrawal

```sql
INSERT INTO Withdrawal
VALUES (1, 101, 2000);
```

---

## Test Deposit

```sql
INSERT INTO Deposit
VALUES (1, 101, 1000);
```

---

## Test Transaction

```sql
INSERT INTO Transactions
VALUES (1, 101, 'Withdraw', 2000, SYSDATE);
```

---

# Concepts Used

- BEFORE Trigger
- AFTER Trigger
- Row-Level Trigger
- Trigger with Conditions
- Trigger using Sequence
- Audit Trigger
- Validation Trigger
- Automatic Update Trigger

---

# Simple Understanding

| Concept | Meaning |
|---|---|
| BEFORE Trigger | Runs before operation |
| AFTER Trigger | Runs after operation |
| :NEW | New value |
| :OLD | Old value |
| Sequence | Auto-generates numbers |
| Trigger | Automatic action |

---

# Conclusion

Successfully implemented database triggers to validate data, automate balance updates, maintain audit logs, and enforce banking rules automatically.
