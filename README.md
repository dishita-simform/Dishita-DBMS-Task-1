
# SQL DBMS Task

This Task involves creating and managing an EMPLOYEE database with two tables: EmployeeInfo and EmployeePosition. It includes database creation, table creation, data insertion, and executing various SQL queries.

# SQL Queries

1. Create DataBase

```sql
CREATE DATABASE EMPLOYEE;
```
2. Create Tables

```sql
CREATE TABLE EmployeeInfo (
    EmpID SERIAL PRIMARY KEY,
    EmpFname VARCHAR(50) NOT NULL,
    EmpLname VARCHAR(50) NOT NULL,
    Department VARCHAR(20) NOT NULL,
    Project VARCHAR(10) NOT NULL,
    Address VARCHAR(100) NOT NULL,
    DOB DATE NOT NULL,
    Gender CHAR(1) NOT NULL
);

CREATE TABLE EmployeePosition (
    EmpID INT REFERENCES EmployeeInfo(EmpID) UNIQUE,
    EmpPosition VARCHAR(20),
    DateOfJoining DATE NOT NULL,
    Salary INT
);
```
3. Insert Data
```sql
INSERT INTO EmployeeInfo (EmpFname, EmpLname, Department, Project, Address, DOB, Gender) VALUES
('Sanjay', 'Mehra', 'HR', 'P1', 'Hyderabad(HYD)', '1976-12-01', 'M'),
('Ananya', 'Mishra', 'Admin', 'P2', 'Delhi(DEL)', '1968-05-02', 'F'),
('Rohan', 'Diwan', 'Account', 'P3', 'Mumbai(BOM)', '1980-01-01', 'M'),
('Sonia', 'Kulkarni', 'HR', 'P1', 'Hyderabad(HYD)', '1992-05-02', 'F'),
('Ankit', 'Kapoor', 'Admin', 'P2', 'Delhi(DEL)', '1994-07-03', 'M');

INSERT INTO EmployeePosition (EmpID, EmpPosition, DateOfJoining, Salary) VALUES
(1, 'Manager', '2022-05-01', 500000),
(2, 'Executive', '2022-05-02', 75000),
(3, 'Manager', '2022-05-01', 90000),
(4, 'Lead', '2022-05-02', 85000),
(5, 'Executive', '2022-05-01', 300000);
```
4. Count Employees in Admin Department
```sql
SELECT COUNT(*) AS "No of employees in Admin" FROM EmployeeInfo WHERE Department='Admin';
```
5. Retrieve First 4 Characters of Last Names
```sql
SELECT SUBSTRING(EmpLname,1,4) AS "EmpLname" FROM EmployeeInfo;
```
6. Find Employees with a Salary between 50,000 and 100,000
```sql
SELECT * FROM EmployeeInfo ei 
JOIN EmployeePosition ep ON ei.EmpID = ep.EmpID 
WHERE ep.Salary BETWEEN 50000 AND 100000;
```
7. Find Employees whose First Name starts with "S"
```sql
SELECT EmpFname FROM EmployeeInfo WHERE EmpFname LIKE 'S%';
```
8. Fetch Top N Records ordered by Salary
```sql
SELECT * FROM EmployeePosition ORDER BY Salary DESC LIMIT 5;
```
9. Exclude Employees with First Names "Sanjay" and "Sonia" 
```sql
SELECT * FROM EmployeeInfo WHERE EmpFname NOT IN ('Sanjay', 'Sonia');
```
10. Department-Wise count of Employees sorted by Count
```sql
SELECT Department, COUNT(*) AS "NoOfEmployees" 
FROM EmployeeInfo 
GROUP BY Department 
ORDER BY COUNT(*);
```
11. Create an Index on Last Name for Optimized Searches
```sql
CREATE INDEX idx_dep_name ON EmployeeInfo(Department);
```
