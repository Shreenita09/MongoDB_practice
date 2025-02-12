

1. Operators:

show databases;
use vit;
show tables from vit;
select * from cse;
insert into cse values (1002,'jayanth',78);
insert into cse values (1011,'Arin',85,'UK');
desc cse;
ALTER TABLE cse DROP COLUMN s_contact;
ALTER TABLE cse ADD(
    s_country varchar(25) DEFAULT 'India'
);
use vit;
ALTER TABLE cse RENAME column 
    s_country TO s_state;
desc cse;
select * from cse;
delete from cse where s_id=1002;
insert into cse values (1002,'Jayanth',75,'India'),(1003,'Tamilarasan',85,'India');
UPDATE cse SET s_name='Vishnu' WHERE s_id=1002;
UPDATE cse SET s_mark = s_mark+1; 
use vit;
select s_id,S_name from cse where s_id=1002;
use org123;
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
desc persons;
ALTER TABLE Persons
MODIFY Age int NOT NULL;
CREATE TABLE Persons1 (
    ID int primary key,
    LastName varchar(255) NOT NULL unique,
    FirstName varchar(255) NOT NULL unique,
    Age int
);
desc persons1;
use org123;
create table category(
c_id int primary key,
c_name varchar(25) not null unique,
c_decrp varchar(250) not null
);
insert into category values (102, 'furnitures', 'it stores all set of wooden items');
select * from category;
desc category;
use org123;
CREATE TABLE Products (
    P_ID int primary key,
    p_Name varchar(250) NOT NULL,
    c_id int ,
    CONSTRAINT c_id FOREIGN KEY (c_id)
    REFERENCES category(c_id)
);
show tables from org123;
desc products;
drop table products;
insert into products values (904, 'Wooden table', null);
select * from products;
select * from category;
delete from category where c_id=101;
drop table category;
CREATE TABLE Course (
    cno INT PRIMARY KEY,
    cname VARCHAR(20)
);
select * from course;
INSERT INTO Course(cno, cname) 
 VALUES(101,'c'),
       (102,'c++'),
       (103,'DBMS');
CREATE TABLE Enroll (
    sno INT,
    cno INT,
    jdate date,
    PRIMARY KEY(sno),
    FOREIGN KEY(cno) 
        REFERENCES Course(cno)
        ON DELETE CASCADE
);
INSERT INTO Enroll(sno,cno,jdate) 
 VALUES(2, 105, "2021/05/05");
select * from enroll;
desc enroll;
create database saturday;
use saturday;
create table category(
c_id int primary key,
c_name varchar(25) not null unique,
c_decrp varchar(250) not null
);
insert into category values (101, 'electronics', 'it stores all set of electronics items');
select * from category;
desc category;
CREATE TABLE Products (
    P_ID int primary key,
    p_Name varchar(250) NOT NULL,
    c_id int ,
    CONSTRAINT c_id FOREIGN KEY (c_id)
    REFERENCES category(c_id) on delete cascade
);
insert into products values (904, 'INTEL I5 Processor', 101);
select * from products;
delete from category where c_id=101;
select * from category;
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (salary>=200000 and salary <=400000)
);
ALTER TABLE Persons	
ADD CHECK (Age>=18);
CREATE TABLE Persons1 (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Coimbatore'
);
desc persons1;
use org123;
show tables from org123;
select * from worker;
SELECT * FROM worker WHERE salary LIKE '8%';
use org123;
create view admin_more_salary as 
select * from worker 
where department='Admin' and salary > 100000 order by salary desc;
select * from admin_more_salary;
select department, count(department) from worker 
where department in ('admin','account') group by department;
SELECT department, COUNT(department) as highest_head_count
FROM worker
GROUP BY department
HAVING COUNT(department) >= 3;
create table vitBhopal (id int primary key, name varchar(20) not null,
department varchar(25) not null);
insert into vitbhopal values (104,'Karthik','cs'),(103,'Arun','cs');
create table vit (id int primary key, name varchar(20) not null,
college varchar(25) not null);
insert into vit values (104,'Karthik','chennai'),(103,'Arun','bhopal');
select * from vit;
select * from vitbhopal;
select name as WinnerOfTheYear from vitbhopal
where id = (select id from vit where college='bhopal');
use org123;
drop table student;
create table student(
s_id int primary key,
s_name varchar(25) not null,
s_department varchar(25) not null
);
insert into student values (1001,"Jayanth","ECE"),(1002,"Praveen","CSE"),(1003,"Logesh","Mech"),(1006,'karthick','Aero'),(1007,"Mahesh","Civil");
select * from student;
drop table vit;
create table VIT(
s_id int primary key,
s_cgpa varchar(5) not null
);
insert into vit values (1001,'7.2'),(1002,'8.6'),(1007,'9.25');
select * from vit;
use org123;
select * from student cross join vit;
SELECT * from student INNER JOIN vit where student.s_id = vit.s_id;
SELECT * FROM student full outer JOIN vit ON (student.s_id = vit.s_id);
CREATE DATABASE practise;
USE practise;

CREATE TABLE Worker (
    WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    FIRST_NAME CHAR(25),
    LAST_NAME CHAR(25),
    SALARY INT,
    JOINING_DATE DATETIME,
    DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
    (WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
    (1, 'Monika', 'Arora', 100000, '2014-02-20 09:00:00', 'HR'),
    (2, 'Niharika', 'Verma', 80000, '2014-06-11 09:00:00', 'Admin'),
    (3, 'Vishal', 'Singhal', 300000, '2014-02-20 09:00:00', 'HR'),
    (4, 'Amitabh', 'Singh', 500000, '2014-02-20 09:00:00', 'Admin'),
    (5, 'Vivek', 'Bhati', 500000, '2014-06-11 09:00:00', 'Admin'),
    (6, 'Vipul', 'Diwan', 200000, '2014-06-11 09:00:00', 'Account'),
    (7, 'Satish', 'Kumar', 75000, '2014-01-20 09:00:00', 'Account'),
    (8, 'Geetika', 'Chauhan', 90000, '2014-04-11 09:00:00', 'Admin');
    
select * from Worker;

SELECT * FROM Worker WHERE SALARY=100000 AND DEPARTMENT ='HR';

SELECT * FROM Worker WHERE SALARY > 200000;

SELECT * FROM Worker WHERE SALARY=100000 AND DEPARTMENT = 'HR';

SELECT * FROM Worker WHERE SALARY between 100000 AND 200000;

SELECT * FROM Worker WHERE SALARY not between 100000 AND 200000;

SELECT * FROM worker
WHERE SALARY BETWEEN 200000 AND 400000
AND WORKER_ID in (1,2,3);

desc worker;

SELECT * FROM Worker 
WHERE DEPARTMENT = 'HR' 
ORDER BY SALARY ASC;


SELECT FIRST_NAME, LAST_NAME  
FROM Worker  
WHERE DEPARTMENT = 'HR'  
AND SALARY = (SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT = 'HR');

SELECT DEPARTMENT, FIRST_NAME, LAST_NAME, SALARY
FROM Worker w
WHERE SALARY = (
    SELECT MAX(SALARY) 
    FROM Worker 
    WHERE DEPARTMENT = w.DEPARTMENT
);

SELECT COUNT(*) AS Total_Workers
FROM Worker;

SELECT COUNT(*) AS HR_Workers
FROM Worker
WHERE DEPARTMENT = 'HR';

SELECT AVG(SALARY) AS Average_Salary
FROM Worker;

SELECT AVG(SALARY) AS Admin_Avg_Salary
FROM Worker
WHERE DEPARTMENT = 'Admin';

SELECT SUM(SALARY) AS Total_Salary
FROM Worker;

SELECT SUM(SALARY) AS HR_Total_Salary
FROM Worker
WHERE DEPARTMENT = 'HR';

SELECT * FROM Worker
WHERE (DEPARTMENT = 'Admin' OR DEPARTMENT = 'Account')
and SALARY = (SELECT MIN(SALARY) FROM Worker WHERE Salary = (SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT in ('Admin','Account'))
);



2. Savepoint-Commit

show databases;

create database practise;

use practise;

show tables;

CREATE TABLE Mech (
    s_id INT, 
    s_name VARCHAR(25)
);

START TRANSACTION;

    INSERT INTO Mech VALUES (101, 'Jayanth');
    SAVEPOINT A;
    
    UPDATE Mech SET s_id = 102 WHERE s_id = 101;
    SAVEPOINT B;
    
    INSERT INTO Mech VALUES (103, 'Karthick');
    SAVEPOINT C;
    
    SELECT * FROM Mech;
    
    ROLLBACK TO SAVEPOINT B;
    
    SELECT * FROM Mech;
    
COMMIT;

SET SQL_SAFE_UPDATES = 1;




Week 2

1. Case Statement:
	
show databases;

use practise;

select * from worker;

SELECT worker_id, first_name,department,
CASE
    WHEN salary > 300000 THEN 'Rich people'
    WHEN salary <=300000 && salary >=100000 THEN 'Middle stage'
    ELSE 'Poor people'
END 
AS People_stage_wise 
from worker;


2. order by-group by:

show databases;

use practise;

select * from worker where department = 'Admin' order by department desc;

select * from worker where department = 'Admin' order by department desc limit 3;

select department, count(DEPARTMENT) as total_employees  from worker 
where department = 'HR' or DEPARTMENT='account' group by department;

select department, count(department) as total_employees from worker
group by department
order by total_employees desc Limit 2;

(
  SELECT department, COUNT(department) AS total_employees
  FROM worker
  GROUP BY department
  ORDER BY total_employees ASC
  LIMIT 1
)

UNION ALL

(
  SELECT department, COUNT(department) AS total_employees
  FROM worker
  GROUP BY department
  ORDER BY total_employees DESC
  LIMIT 1
);


3. Not Null-Primary key:

use practise;

create table Persons (
	ID int PRIMARY KEY not null,
    first_name varchar(255) not null,
    last_name varchar(255) not null,
    Unique(ID)
);

desc persons;

4. Cascade:
use practise;

create table category(
c_id int primary key,
c_name varchar(25) not null unique,
c_decrp varchar(250) not null
);

insert into category values (101, 'electronics', 'it stores all set of electronics items');
select * from category;
desc category;

CREATE TABLE Products (
    P_ID int primary key,
    p_Name varchar(250) NOT NULL,
    c_id int ,
    CONSTRAINT c_id FOREIGN KEY (c_id)
    REFERENCES category(c_id) on delete cascade
);

insert into products values (904, 'INTEL I5 Processor', 101);
select * from products;

delete from category where c_id=101;
select * from category;

select * from worker;

CREATE TABLE Bonus (
	WORKER_REF_ID INT,
	BONUS_AMOUNT INT(10),
	BONUS_DATE DATETIME,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES Worker(WORKER_ID)
        ON DELETE CASCADE
);

INSERT INTO Bonus 
	(WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
		(001, 5000, '16-02-20'),
		(002, 3000, '16-06-11'),
		(003, 4000, '16-02-20'),
		(001, 4500, '16-02-20'),
		(002, 3500, '16-06-11');
        
SELECT department, COUNT(*) AS department_count
FROM worker
GROUP BY department
ORDER BY department_count DESC
LIMIT 1 OFFSET 1;

(SELECT * FROM Worker ORDER BY worker_ID DESC LIMIT 5)
ORDER BY worker_ID ASC;

desc worker;

CREATE TABLE Title (
	WORKER_REF_ID INT,
	WORKER_TITLE CHAR(25),
	AFFECTED_FROM DATETIME,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES Worker(WORKER_ID)
        ON DELETE CASCADE
);


INSERT INTO Title (WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) 
VALUES
 (1, 'Manager', '2016-02-20 00:00:00'),
 (2, 'Executive', '2016-06-11 00:00:00'),
 (8, 'Executive', '2016-06-11 00:00:00'),
 (5, 'Manager', '2016-06-11 00:00:00'),
 (4, 'Asst. Manager', '2016-06-11 00:00:00'),
 (7, 'Executive', '2016-06-11 00:00:00'),
 (6, 'Lead', '2016-06-11 00:00:00'),
 (3, 'Lead', '2016-06-11 00:00:00');




Week 3

1. Having Clause:
2. Joints:
use practise;

create table student(
s_id int primary key,
s_name varchar(25) not null,
s_department varchar(25) not null
);

insert into student values (1001,"Jayanth","ECE"),(1002,"Praveen","CSE"),(1003,"Logesh","Mech"),(1006,'karthick','Aero'),(1007,"Mahesh","Civil");

select * from student;

drop table vit;

create table VIT(
s_id int primary key,
s_cgpa varchar(5) not null
);

insert into vit values (1001,'7.2'),(1002,'8.6'),(1007,'9.25');

select * from vit;

select * from student cross join vit;

SELECT student.s_id, student.s_name, student.s_department, vit.s_cgpa
FROM student 
INNER JOIN vit 
ON student.s_id = vit.s_id;

SELECT student.s_id, student.s_name, student.s_department, vit.s_cgpa
FROM student 
LEFT JOIN vit 
ON student.s_id = vit.s_id;

SELECT student.s_id, student.s_name, student.s_department, vit.s_cgpa
FROM student
RIGHT JOIN vit ON student.s_id = vit.s_id;

SELECT student.s_id, student.s_name, student.s_department, vit.s_cgpa
FROM student
FULL JOIN vit ON student.s_id = vit.s_id;


show tables;

select * from worker;

select * from title;

select * from worker
INNER JOIN title on worker.WORKER_ID=title.WORKER_REF_ID
where title.worker_title="manager";






    
