# Stored Procedure in SQL

## Aim
To perform various Stored Procedure operations using the Hospital Management System database.

---

# Tables Used

## Patient
- patient_id
- patient_name
- age
- gender
- contact_no

## Doctor
- doctor_id
- doctor_name
- specialization
- fees

## Appointment
- appointment_id
- patient_id
- doctor_id
- appointment_date

## Billing
- bill_id
- patient_id
- total_amount
- billing_date

---

# Step 1: Create Tables

```sql
CREATE TABLE Patient (
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(50),
    age INT,
    gender VARCHAR(10),
    contact_no VARCHAR(15)
);

CREATE TABLE Doctor (
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(50),
    specialization VARCHAR(50),
    fees DECIMAL(10,2)
);

CREATE TABLE Appointment (
    appointment_id INT PRIMARY KEY,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE,
    FOREIGN KEY (patient_id) REFERENCES Patient(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctor(doctor_id)
);

CREATE TABLE Billing (
    bill_id INT PRIMARY KEY,
    patient_id INT,
    total_amount DECIMAL(10,2),
    billing_date DATE,
    FOREIGN KEY (patient_id) REFERENCES Patient(patient_id)
);
```

---

# Step 2: Insert Sample Records

```sql
INSERT INTO Patient VALUES (101, 'Aarya', 20, 'Male', '9876543210');
INSERT INTO Patient VALUES (102, 'Sneha', 21, 'Female', '9876501234');

INSERT INTO Doctor VALUES (1, 'Dr. Sharma', 'Cardiologist', 1000);
INSERT INTO Doctor VALUES (2, 'Dr. Mehta', 'Dermatologist', 800);
```

---

# 1. Procedure to Add Patient

```sql
CREATE OR REPLACE PROCEDURE Add_Patient(
    p_id INT,
    p_name VARCHAR,
    p_age INT,
    p_gender VARCHAR,
    p_contact VARCHAR
)
AS
BEGIN
    INSERT INTO Patient
    VALUES (p_id, p_name, p_age, p_gender, p_contact);
END;
/
```

## Execute Procedure

```sql
EXEC Add_Patient(103, 'Rahul', 25, 'Male', '9999999999');
```

---

# 2. Procedure to Display Patient Details

```sql
CREATE OR REPLACE PROCEDURE Show_Patient
AS
BEGIN
    FOR rec IN (SELECT * FROM Patient)
    LOOP
        DBMS_OUTPUT.PUT_LINE(rec.patient_id || ' ' || rec.patient_name);
    END LOOP;
END;
/
```

## Execute Procedure

```sql
EXEC Show_Patient;
```

---

# 3. Procedure to Insert Doctor Details

```sql
CREATE OR REPLACE PROCEDURE Add_Doctor(
    d_id INT,
    d_name VARCHAR,
    d_spec VARCHAR,
    d_fees DECIMAL
)
AS
BEGIN
    INSERT INTO Doctor
    VALUES (d_id, d_name, d_spec, d_fees);
END;
/
```

## Execute Procedure

```sql
EXEC Add_Doctor(3, 'Dr. Patil', 'Neurologist', 1500);
```

---

# 4. Procedure to Schedule Appointment

```sql
CREATE OR REPLACE PROCEDURE Schedule_Appointment(
    a_id INT,
    p_id INT,
    d_id INT,
    a_date DATE
)
AS
BEGIN
    INSERT INTO Appointment
    VALUES (a_id, p_id, d_id, a_date);
END;
/
```

## Execute Procedure

```sql
EXEC Schedule_Appointment(1, 101, 1, '12-MAY-2026');
```

---

# 5. Procedure to Generate Billing Record

```sql
CREATE OR REPLACE PROCEDURE Generate_Bill(
    b_id INT,
    p_id INT,
    amount DECIMAL,
    b_date DATE
)
AS
BEGIN
    INSERT INTO Billing
    VALUES (b_id, p_id, amount, b_date);
END;
/
```

## Execute Procedure

```sql
EXEC Generate_Bill(1, 101, 2500, '12-MAY-2026');
```

---

# 6. Procedure to Search Patient by ID

```sql
CREATE OR REPLACE PROCEDURE Search_Patient(
    p_id INT
)
AS
BEGIN
    FOR rec IN (
        SELECT * FROM Patient
        WHERE patient_id = p_id
    )
    LOOP
        DBMS_OUTPUT.PUT_LINE(rec.patient_name || ' ' || rec.contact_no);
    END LOOP;
END;
/
```

## Execute Procedure

```sql
EXEC Search_Patient(101);
```

---

# 7. Display Doctor-wise Patient List

```sql
SELECT d.doctor_name, p.patient_name
FROM Appointment a
JOIN Doctor d
ON a.doctor_id = d.doctor_id
JOIN Patient p
ON a.patient_id = p.patient_id;
```

---

# 8. Calculate Total Billing Amount for Patient

```sql
SELECT patient_id, SUM(total_amount) AS Total_Bill
FROM Billing
GROUP BY patient_id;
```

---

# 9. Display Appointment History

```sql
SELECT *
FROM Appointment
WHERE patient_id = 101;
```

---

# 10. Procedure to Update Patient Details

```sql
CREATE OR REPLACE PROCEDURE Update_Patient(
    p_id INT,
    new_contact VARCHAR
)
AS
BEGIN
    UPDATE Patient
    SET contact_no = new_contact
    WHERE patient_id = p_id;
END;
/
```

## Execute Procedure

```sql
EXEC Update_Patient(101, '8888888888');
```

---

# 11. Procedure to Delete Patient Record

```sql
CREATE OR REPLACE PROCEDURE Delete_Patient(
    p_id INT
)
AS
BEGIN
    DELETE FROM Billing WHERE patient_id = p_id;
    DELETE FROM Appointment WHERE patient_id = p_id;
    DELETE FROM Patient WHERE patient_id = p_id;
END;
/
```

## Execute Procedure

```sql
EXEC Delete_Patient(103);
```

---

# Concepts Used

- CREATE PROCEDURE
- IN Parameters
- OUT Parameters
- Procedure Calling
- SELECT Statement in Procedure
- INSERT using Procedure
- UPDATE using Procedure
- DELETE using Procedure

---

# Conclusion

Successfully performed various stored procedure operations in SQL for managing hospital records, appointments, billing, and patient information.
