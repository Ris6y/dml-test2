drop database if exists interview_commands_practice;
create database interview_commands_practice;
use interview_commands_practice;
set autocommit = 1;
create table employees (
employee_id int primary key,
employee_name varchar(60),
department varchar(30),
city varchar(40),
salary decimal (10,2),
employment_status varchar(15),
phone varchar(15)
) engine = InnoDB;
insert into employees
(employee_id, employee_name, dapartment, city, salary, employment_status, phone)

values
    (1, 'Rahul Sharma', 'IT', 'Delhi', 45000.00, 'Active', '9000000001'),
    (2, 'Priya Verma', 'HR', 'Mumbai', 42000.00, 'Active', '9000000002'),
    (3, 'Amit Patel', 'Sales', 'Ahmedabad', 38000.00, 'Inactive', '9000000003'),
    (4, 'Anjali Singh', 'IT', 'Kolkata', 50000.00, 'Active', '9000000004'),
    (5, 'Vijay Kumar', 'Finance', 'Bangalore', 55000.00, 'Active', '9000000005'),
    (6, 'Sanjay Reddy', 'Sales', 'Hyderabad', 36000.00, 'Active', '9000000006'),
    (7, 'Megha Iyer', 'IT', 'Chennai', 48000.00, 'Active', '9000000007'),
    (8, 'Neha Gupta', 'HR', 'Delhi', 32000.00, 'Inactive', '9000000008'),
    (9, 'Arjun Mehta', 'Finance', 'Pune', 52000.00, 'Active', '9000000009'),
    (10, 'Pooja Shah', 'Sales', 'Mumbai', 40000.00, 'Active', '9000000010');
  select * from employees  
    commit;
    
-- Question1

insert into employees
(employee_id, employee_name, department, city, salary, employment_status, phone)
values
(11, 'Karan Malhotra', 'IT', 'Noida', 41000.00, 'Active', '90000000011');

select*
from employees
where employee_id = 11;

-- Question 2

insert into employees
(employee_id, employee_name, department, city, salary, employment_status, phone)
values
(12,'Simran Kaur', 'HR', 'Delhi', 35000.00, 'Active', '9000000012')
(13, 'Rohan Das', 'Sales', 'Pune', 33000.00, 'Inactive', '9000000013');

select*
from employees
where employee_id in (12,13);

-- Question 3 

update employees
set city = n'Gurgaon',
salary = 46000.00
where employee_id = 11;

select *
from employees
where employee_id = 11;

-- Question 4

update employees
set salary = salary * 1.10
where employee_id in (1, 4, 7);

select employee_id, employee_name, salary
from employees
where employee_id in (1, 4, 7); 

-- Question 5 

delete from employees
where employee_id in (3, 8, 13);

select * 
from employees
where employee_id in (3, 8, 13);

select *
from employees;

-- Question 6 

alter table employees
add column email varchar(100) null;

describe employees;

select * from employees;

-- Question 7 

alter table employees
modify column phone varchar(100) null;

describe employees;

select employee_id, employee_name, phone
from employees;

-- Question 8 

alter table employees
rename column city to work_city;

describe employees;

select employee_id, emplotee_name, work_city
from employees;

-- Question 9

alter table employees
drop column email;

describe employees;

select *
from employees;

-- Question 10

rename table employee to staff;

show tables;

describe staff;

select *
from staff;

-- Question 11

start transaction;

-- insert a new employee into staff
insert into staff
(employee_id, employee_name, department, work_city, salary, employment_status, phone)
values
(14, 'NISHA RAO', 'ID', 'NOIDA', 44000.00, 'ACTIVE', '9000000014');

-- UPDATE THE SALARY OF EMPLOYEE ID 2
UPDATE STAFF
SET SALARY = 45000.00
WHERE EMPLOYEE_ID = 2;

-- SAVE BOTH CHANGES PERMANENTLY
COMMIT;

ROLLBACK;

select * 
FROM staff
where employee_id = 14;

select employee_id, employee_name, salary
from staff
where employee_id = 2;

-- Question 12 

start transaction;

update staff
set salary = 60000.00
where employee_id = 5;

delete from staff
where employee_id = 6;

ROLLBACK;

select employee_id, employee_name, salary
from staff
where employee_id = 5;

select *
from staff
where employee_id = 6;

-- Question 13

start transaction;

update staff
set salary = 47000.00
where employee_id = 14;

savepoint salary_saved;

update staff
set work_city = 'jaipur'
where employee_id = 14;

savepoint city_saved;

delete from staff
where employee_id = 14;

rollback to savepoint city_saved;

rollback to savepoint salary_saved;

commit;

select employee_id, employee_name, work_city, salary
from staff
where employee_id = 14;

savepoint savepoint_name;
rollback to savepoint savepoint_name;

commit;

-- Question 14

start transaction;

-- Remove all rows from staff
truncate table staff;

-- Attempt to undo the operation
rollback;

select *
from staff;

describe staff;

-- Question 15 

drop table staff; 
