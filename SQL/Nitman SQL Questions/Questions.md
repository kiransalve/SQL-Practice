CREATE TABLE em (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10, 2),
    hire_date DATE
);

INSERT INTO em (emp_id, emp_name, department, salary, hire_date, manager_id)
VALUES
(1, 'Alice', 'HR', 55000, '2018-01-15',2),
(2, 'Bob', 'IT', 75000, '2017-05-23',null),
(3, 'Charlie', 'Finance', 82000, '2019-03-12',2),
(4, 'Diana', 'IT', 60000, '2020-07-19',2),
(5, 'Eve', 'HR', 52000, '2021-11-05',12),
(6, 'Frank', 'Finance', 72000, '2020-08-10',12),
(7, 'Grace', 'HR', 61000, '2016-12-20',12),
(8, 'Hank', 'IT', 69000, '2019-01-11',12),
(9, 'Ivy', 'Finance', 73000, '2018-09-30',12),
(10, 'Jack', 'HR', 54000, '2017-10-15',12),
(11, 'Kate', 'IT', 78000, '2016-06-01',12),
(12, 'Leo', 'HR', 59000, '2019-02-21',null),
(13, 'Mia', 'Finance', 76000, '2019-04-10',12),
(14, 'Nick', 'IT', 65000, '2018-12-05',12),
(15, 'Olivia', 'HR', 53000, '2020-09-29',12),
(16, 'Paul', 'Finance', 70000, '2021-03-22',12),
(17, 'Quincy', 'IT', 72000, '2020-01-07',12),
(18, 'Rita', 'HR', 60000, '2020-05-15',19),
(19, 'Steve', 'Finance', 78000, '2019-08-18',null),
(20, 'Tom', 'IT', 81000, '2018-07-23',19),
(21, 'Uma', 'HR', 58000, '2020-02-17',19),
(22, 'Victor', 'Finance', 75000, '2021-05-10',19),
(23, 'Wendy', 'IT', 70000, '2020-10-05',19),
(24, 'Xander', 'HR', 62000, '2017-11-22',19),
(25, 'Yara', 'Finance', 82000, '2021-06-30',19);

CREATE TABLE manager (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10, 2),
    hire_date DATE
);

INSERT INTO manager (emp_id, emp_name, department, salary, hire_date)
VALUES
(2, 'Bob', 'IT', 75000, '2017-05-23'),
(12, 'Leo', 'HR', 59000, '2019-02-21'),
(19, 'Steve', 'Finance', 78000, '2019-08-18');

-- 1. create department wise salary table from emp table
create table dws
as 
(select department, sum(salary) from em
group by department); 
select * from dws;

-- 2. create table with same data as emp
create table em2 as (select * from em);  
select * from em2;

-- 3. display 2nd/3rd/nth highest salary

-- using sub query

SELECT max(salary) from em
where salary < 
(select max(salary) from em
where salary < 
(select max(salary) from em
));

-- using limit
select salary from em
order by salary desc limit 2, 1;

-- using limit and offset
select salary from em
order by salary desc
limit 1 offset 2;

-- using distinct 
select salary from em e1
where 2 = (
select count(DISTINCT(e2.salary)) from em e2
where e2.salary > e1.salary);

--  display all manager name 
select * from em
where (emp_id in (select manager_id from em));

-- display name start with "A"
select * from em where emp_name like "A%";

-- display current date
select curdate();
select current_date();
select current_date;
select date(now());
select date(current_timestamp());

-- display alternate records
-- even
select * from em where emp_id % 2 = 0;
-- odd
select * from em where emp_id % 2 = 1;

-- using row_number
select * from 
(select *, 
ROW_NUMBER() over(ORDER BY emp_id) as row_num
from em) e
where e.row_num % 2 = 0;

-- common records from two tables
select * from em
inner join manager m on em.emp_id = m.emp_id;

-- duplicate records
select salary from em
group by salary
having count(*) > 1;

-- delete duplicate records
select * from em1;

delete e1 
from em1 e1
inner join em1 e2
where e1.emp_id < e2.emp_id 
and e1.emp_name = e2.emp_name;  

-- using group by
-- https://www.youtube.com/watch?v=h48xzQR3wNQ

delete from em2 
where emp_id not in (
	select min(emp_id)
    from em2
    group by emp_name);

-- using windows function
delete from cars
where id in (
select id from (
select *, row_number() over(PARTITION BY model, brand) as rn
from cars) as t
where rn > 1);


-- nth records from 
-- select * from em limit N-1,1;
select * from em limit 3,1;

-- select * from em limit 1 offset N-1;
select * from em limit 1 offset 0; 

-- first 5 records
select * from em limit 5;

-- last 5 records
-- method - 1 
(select * from em
order by emp_id desc limit 5)  order by emp_id ASC;

-- method - 2
select * from em
where emp_id > (select max(emp_id) - 5 from em);
 
-- method - 3
select * from em
where emp_id >
(select count(*) from em) - 5;

-- find first record
select * from em limit 1;

select * from em
where emp_id = (
select min(emp_id) from em);

-- last record
select * from em order by emp_id desc LIMIT 1;
 
select * from em
WHERE emp_id = (select max(emp_id) from em); 

-- get distict record without using distict
select salary from em
group by salary;

select department from em
UNION
select department from em;
    
-- maximum salary each department
select department, max(salary), round(avg(salary),0) from em
group by department;

-- deprtment wise salary 
select department, count(*) from em
group by department
order by count(*);

-- change data type of column
ALTER table em 
modify emp_id INT;

select * from em;

DESCRIBE em; 

-- What are tables and fields
-- table is organised collection of data stored in form of rows and columns 
-- columns are called as field and rows are records

-- difference between unique key , foreign key and primary key
-- unique values are uniquely identifies the each records, included null values only one value per column
-- primary key are unique key without null values
-- one table can have muliple unique keys but only one primary keys
-- we can not change or delete the primary key column value but we can modify unique key values.
-- foreign key used to link one or more table.

-- what is select statement?
-- select operator is used to fetch data from database
-- data return is stored in a result table called result set
-- select is data manipulation language (DML) command

-- which are claused we use with select statement?
-- from - it defines table from which data should be fetch
-- where - use to filter records
-- order by - sorting data 
-- group by - it group record with identical records , can be use to summarize results from database
-- having - it filter the aggregated records, use with group by clause

-- what are joins? and types
-- joins are used to retrive data from multiple tables into meaningful result set
-- there are four types - inner join, self join, outer join (left/right/full), cross join
-- inner = common from both 
-- self = used to join a table with it self, we use it to combine data with other data of same table
-- cross = combin each row of first with each row of second table, like cartession product
-- outer = used to combine data from other table based on common column

-- difference between truncate, delete and drop?
-- delete = remove some or all rows from table based on the condition, it can roll back, 
--  table structure stays
delete from em
where emp_id >10;

begin;
delete from em
where emp_id >10;
ROLLBACK;

-- TRUNCATE - remove all rows from table
-- no where clause allowed
-- table structure stays
-- can not roll back
-- faster that delete


-- drop - delete entire table
-- remove data and structure
-- can not be roll back

-- what is "Alias" in sql?
-- provide another name to table or column which are more convenient to use and readable

-- what are constraint?
-- it is rule you put on table to control what data is allowed 
-- it stops invalid data, protect relationship between table and prevent duplicate
-- Primary key, Foreign Key, Unique, Not Null, check, Default

-- difference between having and where?
-- where used to filter rows, and having used to filter row after grouping
-- where can not used with aggregate function, having can use 

-- difference between "IN" and "between"?
-- BETWEEN - Used to match a range of values
-- Includes both start and end values (inclusive)
-- Mostly used with numbers and dates           

select *
from em
where salary between 30000 and 60000;

-- IN - Used to match multiple specific values
-- Best when you know exact values
-- Works with numbers, strings, dates, subqueries 

select * from em
where department in ("HR", "IT");

-- what is distinct? 
select distinct(manager_id) from em;

-- what are subset of sql?
-- DDL - Data definition Language - it define the data structure
-- DDL commands - create, alter, drop, truncate, comment and rename

-- DML - Data Manipulation Language - use to modify, retrive and delete data 
-- DML commands - select, insert, update, delete

-- DCL - Data Control Language - concern to rights and permission to get access of database
-- DCL commands - grant, revoke

-- TCL - Tranzaction contril Language
-- TCL commands - commit, rollback, savepoint, set tranzaction

-- what is RDBMS
-- Relational Database Management System that store data in the form of collection of tables
-- MySQL, SQL Server, Oracle database

-- how to get remainder in division operator?
select mod(27,5) as 'value';

-- difference between union and union all?
-- union remove duplicate, union all does not remove duplicate

-- intersect used to get common records from two table

-- ACID property in sql?
/*
Atomicity
All or nothing
A transaction is treated as one unit
If one step fails → everything rolls back

Example:
Money transfer
₹100 debited ❌
₹100 credited ❌
Both must succeed, or neither happens        

Consistency
Data stays correct
Transaction moves DB from one valid state to another
All rules, constraints are followed

Example:
Balance can never become negative if rule exists

Isolation
Transactions don’t disturb each other
Multiple transactions can run at same time
Each behaves as if it’s running alone

Example:
Two users buying the last product → only one succeeds

Durability
Once committed, it stays
After COMMIT, data is permanently saved
Even if system crashes 💥, data remains

-- Normalization - Data is split into multiple related tables
First Normal Form (1NF)
Rule:
No multiple values in one column
Each column has atomic (single) values

Before 1NF -

| order_id | products       |
| -------- | -------------- |
| 1        | Laptop, Mobile |

After 1NF - 

| order_id | product |
| -------- | ------- |
| 1        | Laptop  |
| 1        | Mobile  |

One value per cell

Second Normal Form (2NF) -
Rule:
Must be in 1NF
No partial dependency
Applies when composite primary key exists

Problem
Table with (order_id, product_id) as primary key:

| order_id | product_id | product_name |
| -------- | ---------- | ------------ |
| 1        | 101        | Laptop       |
| 1        | 102        | Mobile       |

product_name depends only on product_id, not full key

After 2NF - 

| order_id | product_id |
| -------- | ---------- |
| product_id | product_name |
| ---------- | ------------ |

No partial dependency

Third Normal Form (3NF) - 

Rule:
Must be in 2NF
No transitive dependency
Non-key columns depend only on primary key

Problem
| emp_id | dept_id | dept_name |
| ------ | ------- | --------- |

dept_name depends on dept_id, not emp_id

After 3NF

| emp_id | dept_id |
| ------ | ------- |

| dept_id | dept_name |
| ------- | --------- |


-- Denormalization - combining tables to improve performance

-- What is a VIEW?
A VIEW is a virtual table created from a SELECT query.
It does not store data, It stores the query
*/

create view high_salary_emp as 
select emp_id, emp_name, salary
from emp 
where salary > 50000;

select * from high_salary_emp;




 
