# MongoDB_practice
-- Create and use databases
CREATE DATABASE Practice1;
USE Practice1;

CREATE TABLE Mech (
    s_id INT,
    s_name VARCHAR(25)
);

CREATE DATABASE ORG123;
USE ORG123;

CREATE TABLE Worker (
    WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    FIRST_NAME CHAR(25),
    LAST_NAME CHAR(25),
    SALARY INT(15),
    JOINING_DATE DATETIME,
    DEPARTMENT CHAR(25)
);

-- Insert Data
INSERT INTO Mech VALUES (101, 'Jayanth'), (103, 'Karthick');

INSERT INTO Worker (WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) 
VALUES
    (001, 'Monika', 'Arora', 100000, '2014-02-20 09:00:00', 'HR'),
    (002, 'Niharika', 'Verma', 80000, '2014-06-11 09:00:00', 'Admin'),
    (003, 'Vishal', 'Singhal', 300000, '2014-02-20 09:00:00', 'HR'),
    (004, 'Amitabh', 'Singh', 500000, '2014-02-20 09:00:00', 'Admin'),
    (005, 'Vivek', 'Bhati', 500000, '2014-06-11 09:00:00', 'Admin'),
    (006, 'Vipul', 'Diwan', 200000, '2014-06-11 09:00:00', 'Account'),
    (007, 'Satish', 'Kumar', 75000, '2014-01-20 09:00:00', 'Account'),
    (008, 'Geetika', 'Chauhan', 90000, '2014-04-11 09:00:00', 'Admin');

-- View Tables
SELECT * FROM Mech;
SELECT * FROM Worker;

-- Filtering
SELECT * FROM Worker WHERE SALARY > 200000;
SELECT * FROM Worker WHERE DEPARTMENT = 'HR';
SELECT * FROM Worker WHERE LAST_NAME LIKE 'S%';
SELECT * FROM Worker WHERE JOINING_DATE BETWEEN '2014-01-01' AND '2014-12-31';

-- Sorting
SELECT * FROM Worker ORDER BY SALARY DESC;
SELECT * FROM Worker ORDER BY FIRST_NAME ASC, LAST_NAME DESC;

-- Grouping & Aggregates
SELECT DEPARTMENT, AVG(SALARY) AS Avg_Salary FROM Worker GROUP BY DEPARTMENT;
SELECT DEPARTMENT, COUNT(WORKER_ID) AS Total_Workers FROM Worker GROUP BY DEPARTMENT HAVING COUNT(WORKER_ID) > 2;

-- CASE Statement
SELECT WORKER_ID, FIRST_NAME, DEPARTMENT,
    CASE
        WHEN SALARY > 300000 THEN 'Rich People'
        WHEN SALARY BETWEEN 100000 AND 300000 THEN 'Middle Stage'
        ELSE 'Poor People'
    END AS People_Stage
FROM Worker;

-- Additional CASE Example
SELECT FIRST_NAME, SALARY,
    CASE
        WHEN SALARY > 400000 THEN 'High Salary'
        WHEN SALARY BETWEEN 200000 AND 400000 THEN 'Moderate Salary'
        ELSE 'Low Salary'
    END AS Salary_Category
FROM Worker;

-- Views
CREATE VIEW Worker_View AS 
SELECT WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, DEPARTMENT 
FROM Worker WHERE SALARY > 100000;
SELECT * FROM Worker_View;

-- Subqueries
SELECT FIRST_NAME, SALARY FROM Worker 
WHERE SALARY > (SELECT AVG(SALARY) FROM Worker);

SELECT FIRST_NAME, DEPARTMENT FROM Worker 
WHERE DEPARTMENT IN (SELECT DISTINCT DEPARTMENT FROM Worker WHERE SALARY > 150000);

-- IN and EXISTS
SELECT * FROM Worker WHERE DEPARTMENT IN ('HR', 'Admin');
SELECT * FROM Worker WHERE EXISTS 
(SELECT 1 FROM Mech WHERE Mech.s_id = Worker.WORKER_ID);

-- LIMIT and OFFSET
SELECT * FROM Worker ORDER BY SALARY DESC LIMIT 5;
SELECT * FROM Worker ORDER BY SALARY DESC LIMIT 5 OFFSET 3;

-- UNION and UNION ALL
SELECT FIRST_NAME, SALARY FROM Worker WHERE SALARY > 100000
UNION
SELECT FIRST_NAME, SALARY FROM Worker WHERE DEPARTMENT = 'Admin';

SELECT FIRST_NAME FROM Worker WHERE DEPARTMENT = 'HR'
UNION ALL
SELECT FIRST_NAME FROM Worker WHERE SALARY > 200000;

-- Indexing
CREATE INDEX idx_salary ON Worker(SALARY);
CREATE INDEX idx_department ON Worker(DEPARTMENT);

-- Finding Department with Highest and Lowest Employees
(
  SELECT department, COUNT(department) AS total_employees
  FROM Worker
  GROUP BY department
  ORDER BY total_employees ASC
  LIMIT 1
)

UNION ALL

(
  SELECT department, COUNT(department) AS total_employees
  FROM Worker
  GROUP BY department
  ORDER BY total_employees DESC
  LIMIT 1
);

-- Deleting Data & Dropping Tables
DELETE FROM Worker WHERE WORKER_ID = 2;
DELETE FROM Worker WHERE SALARY < 90000;
DROP TABLE Mech;
DROP DATABASE Practice1;

