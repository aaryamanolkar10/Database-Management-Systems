**# Department and Employee Management Database**



**## Problem Statement**

**Develop a database for Department and Employee Management.**



**---**



**# 1. E-R Diagram**



**```text**

**+-------------------+         +----------------------+**

**|    Department     |         |       Employee       |**

**+-------------------+         +----------------------+**

**| Department\_ID(PK) |<------->| Employee\_ID (PK)     |**

**| Department\_Name   |    1:M  | Employee\_Name        |**

**+-------------------+         | Salary               |**

&#x20;                             **| Department\_ID (FK)   |**

&#x20;                             **| Contact\_Number       |**

&#x20;                             **+----------------------+**

**```**



**- One department can have many employees.**

**- `Department\_ID` in Employee table acts as a Foreign Key.**



**---**



**# 2. Create Department Table**



**```sql**

**CREATE TABLE Department (**

&#x20;   **Department\_ID NUMBER PRIMARY KEY,**

&#x20;   **Department\_Name VARCHAR2(50) NOT NULL**

**);**

**```**



**---**



**# 3. Create Employee Table**



**```sql**

**CREATE TABLE Employee (**

&#x20;   **Employee\_ID NUMBER PRIMARY KEY,**

&#x20;   **Employee\_Name VARCHAR2(50) NOT NULL,**

&#x20;   **Salary NUMBER(10,2),**

&#x20;   **Department\_ID NUMBER,**



&#x20;   **CONSTRAINT chk\_salary**

&#x20;   **CHECK (Salary > 10000),**



&#x20;   **CONSTRAINT fk\_department**

&#x20;   **FOREIGN KEY (Department\_ID)**

&#x20;   **REFERENCES Department(Department\_ID)**

**);**

**```**



**---**



**# Constraints Applied**



**- `Employee\_ID` → PRIMARY KEY**

**- `Department\_ID` → FOREIGN KEY**

**- `Salary > 10000` → CHECK Constraint**



**---**



**# 4. Insert Valid Records**



**## Insert into Department**



**```sql**

**INSERT INTO Department VALUES (101, 'HR');**

**INSERT INTO Department VALUES (102, 'IT');**

**INSERT INTO Department VALUES (103, 'Finance');**

**```**



**## Insert into Employee**



**```sql**

**INSERT INTO Employee VALUES (1, 'Aarya', 25000, 101);**

**INSERT INTO Employee VALUES (2, 'Rahul', 30000, 102);**

**INSERT INTO Employee VALUES (3, 'Sneha', 28000, 103);**

**```**



**---**



**# 5. Modify Employee Table**



**Add `Contact\_Number` column:**



**```sql**

**ALTER TABLE Employee**

**ADD Contact\_Number VARCHAR2(15);**

**```**



**---**



**# 6. Attempt to Delete Referenced Department**



**```sql**

**DELETE FROM Department**

**WHERE Department\_ID = 101;**

**```**



**## Result**



**The delete operation fails because the department is referenced by employees through a foreign key constraint.**



**Example error:**



**```text**

**ORA-02292: integrity constraint violated - child record found**

**```**



**---**



**# 7. Important SQL Commands**



**## Delete all records but keep table structure**



**```sql**

**DELETE FROM Employee;**

**```**



**OR**



**```sql**

**TRUNCATE TABLE Employee;**

**```**



**---**



**## Delete entire table**



**```sql**

**DROP TABLE Employee;**

**```**



**This removes:**

**- Table structure**

**- All records**

**- Constraints**

**- Indexes**



**---**



**## Delete entire schema/user (Oracle)**



**```sql**

**DROP USER username CASCADE;**

**```**



**This removes:**

**- All tables**

**- Views**

**- Procedures**

**- Entire schema**



**---**



**# Final Tables Structure**



**## Department Table**



**| Department\_ID | Department\_Name |**

**|---|---|**

**| 101 | HR |**

**| 102 | IT |**

**| 103 | Finance |**



**---**



**## Employee Table**



**| Employee\_ID | Employee\_Name | Salary | Department\_ID | Contact\_Number |**

**|---|---|---|---|---|**

**| 1 | Aarya | 25000 | 101 | NULL |**

**| 2 | Rahul | 30000 | 102 | NULL |**

**| 3 | Sneha | 28000 | 103 | NULL |**



**---**

