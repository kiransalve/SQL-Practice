https://www.youtube.com/watch?v=CTLwYjh92xw&list=PLBv9GORP5VkclmbvgNaEB3GBFc-weefX7

1. What are types of SQL Commands ?

SQL has 5 command types: DDL, DML, DQL, DCL, and TCL.


2. How to create new databse in mysql workbench?

Click New SQL Tab (or Ctrl + T)

```
CREATE DATABASE sales_db;
```

click on refresh

** when we write sql commands write in capital letter and when we write database names or columns name , write in small letter **

**best practice :

```
create database if not exists sales;
```

3. How to delete exstisting database in mysql workbench?

```
DROP DATABASE sales_db;
```

**best practice :

```
DROP DATABASE IF EXISTS sales
```

4. How to create tables in mysql workbench?

```
create databse if not exists campusx;

use campusx;

CREATE TABLE users(
user_id INTEGER,
name varchar(255),
email varchar(255),
password varchar(255)
)

```

*** remember - sql commands are in caps and table name and column name in small case

5. How to insert data in tables?

```

insert into users(user_id, name, email, password)
values
(1,"Kiran Salve","kiran@gmail.com","2011"),
(1,"Kiran Salve","kiran@gmail.com","2011"),
(1,"Kiran Salve","kiran@gmail.com","2011");
``` 

6. How to delete tables?

```

truncate table users;  --this empty the table

drop table users;      --this delete the table
```

7. What is Data Integrity?

Data Integrity in SQL means keeping your data accurate, consistent, and reliable throughout its lifecycle.

8. What are Contraints?

Constraints in SQL are rules applied to table columns to enforce data integrity.

Simply: Constraints = Data validation rules at database level

9. How we define Constraints? and what are types?

---1---

```

use campusx;

CREATE TABLE users(
user_id INTEGER NOT NULL,
name varchar(255) NOT null,
email varchar(255) NOT NULL UNIQUE,
password varchar(255) NOT NULL,
);
```


---2---

```

use campusx;

CREATE TABLE users(
user_id INTEGER NOT NULL,
name varchar(255) NOT null,
email varchar(255) NOT NULL,
password varchar(255) NOT NULL,

constraint users_email_unique UNIQUE (name, email) 
);
```

In second way to define Constraint, we have two important benefit,

1. In scenario where we need to make combination of email and password to be unique
   
2. In future when we want to release Constraints on columns, we can simply delete this (users_email_unique)


10. What is auto_increment contraint?

it will increment by 1 for every next row.

11. what is unique contraint?

It ensure the duplicate entry not added for that specific column.

12. What is primary key constraint?

It used to uniquely identify each record

We need not to mention not null and unique seprately when we define primary key

13. What is use case of default contraint?

```

create table ticket(
ticket_id integer primary key,
name varchar(255) not null,
travel_date datetime default current_timestamp
);

O/p

1	kiran	2025-12-18 12:27:32
		
```

14. What is use case of check constraint?

```

create table students(
std_id integer auto_increment primary key,
name varchar(255) not null,
age integer check (age > 6 and age < 25)

constraint students_age check (age > 6 and age < 25)
);

```

15. What is Foreign Key Constraint?

The foreign key is used to create relationship between two tables and maintain data integrity by ensuring that the value in one table must exists in another table.

```
// Parent table
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100)
);

// Child Table
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

1. You cannot insert a value in child table that does not exist in parent
2. Cannot delete parent if child exists

16. Give types of Constraints in SQL?

1. NOT NULL
2. UNIQUE
3. PRIMARY KEY
4. CHECK
5. DEFAULT
6. FOREIGN KEY
7. AUTO_INCREMENT

17. What are referntial actions?

1. Restrict - Stop the action if child records exist.

eg. if one customer has 3 orders then you cannot delete customer

2. CASCADE - Automatically apply the change to child rows

eg. if you delete customer then all orders of that customer deleted
	if you update customer id then order also update the customer id
	
3. SET NULL - set foreign key value to null in child table, FK column must allow NULL

eg. when customer deleted orders are stays and their cid becomes NULL

4. SET Default - set foreign key to any default value like "0"

eg. when customer deleted orders are stays and their cid becomes "0"

18. How to alter columns in tables using alter?

```
-- add columns
ALTER TABLE users
ADD COLUMN city VARCHAR(100),
ADD COLUMN country VARCHAR(100);

-- modify columns
ALTER TABLE users
MODIFY COLUMN name VARCHAR(200);

-- rename columns
ALTER TABLE users
CHANGE COLUMN name full_name VARCHAR(255);

-- delete columns
ALTER TABLE users
DROP COLUMN age;

-- alter constraint
alter table customers
add constraint customer_age check (age > 19);

```

19. What is DDL?

DDL is a set of SQL commands used to create, change, or delete database objects
(like database, table, columns, constraints).

It works on structure, not on data.


```

SELECT * FROM sales.sp;

--  filter column
select model, price, rating from sales.sp;

-- add alias
select os as "Operating Sytem", rating from sales.sp; 

-- mathematical calculation
-- calculate ppi value
select model, 
round(sqrt(resolution_width * resolution_width + 
resolution_height * resolution_height) / screen_size,2) as  ppi from sales.sp;
 
 -- rating scale to 10
 select model, rating/10 from sales.sp;
 
-- create constant column
select model, "samartphone" as "type" from sales.sp;

-- Distinct value from column
-- what are brand names?
select distinct brand_name from sales.sp; 

-- what are os?
select distinct os from sales.sp;

select distinct brand_name, processor_brand
from sales.sp;

-- Filter rows
-- give smartphones that has brand_name?
select * from sales.sp 
where brand_name = "samsung";

-- find all phones with price < 15000
select * from sales.sp
where price < 15000; 

-- between
-- find all phones with price between 10000 to 15000
select * from sales.sp
where price > 10000 and price < 15000;

select * from sales.sp
where price between 10000 and 15000; 
  
-- rating more that 80 and price < 25000
select * from sales.sp
where price < 15000 and rating > 80 and processor_brand = "snapdragon";

-- find all sampsung phone with ram > 8 gb
select * from sales.sp 
where brand_name = "samsung" and ram_capacity > 8;

-- find all phone with snapdrogon samsung
SELECT * from sales.sp
where brand_name = "samsung" and processor_brand ="snapdragon";

-- Query Execution Order
-- FROM
-- JOIN
-- WHERE
-- GROUP BY
-- HAVING
-- SELECT
-- DISTINCT
-- ORDER BY

--  find out brand name which have price more than 100000
SELECT DISTINCT brand_name from sales.sp
WHERE price > 100000;


-- phone of processor snapdragon, bionic 
select * from sales.sp
where processor_brand = "snapdragon" OR
processor_brand = "exynos" OR
processor_brand = "bionic";

select * from sales.sp
where processor_brand in ("snapdragon","exynos","bionic");

select * from sales.sp
where processor_brand not in ("snapdragon","exynos","bionic");

-- Replace snapdragon with snapDG 
UPDATE sales.sp
set processor_brand = "snapDRAGON"
where processor_brand = "snapdragon";

select distinct processor_brand from sales.sp;

update sales.sp
set processor_brand = "HELIO"
where processor_brand = "helio";

update sales.sp
set processor_brand = "BIONIC"
where processor_brand = "bionic";

select * from sales.sp
where price > 200000;

delete from sales.sp
where price > 200000;

SELECT * from sales.sp
where primary_camera_rear > 150 and brand_name = "nokia";

delete from sales.sp
where primary_camera_rear > 150 and brand_name = "nokia";

-- Aggregate function
  
  select max(price) from sales.sp;
  
  select min(price) from sales.sp;
  
  select MAX(ram_capacity) from sales.sp;
  
  -- find costier samsung phone
  
select * from sales.sp
where brand_name = "samsung" and price = 11099;
  
select avg(rating) from sales.sp
where brand_name = "apple";

select avg(price) from sales.sp
where brand_name = "apple";

select count(*) from sales.sp
where brand_name = "apple"; 

select count(distinct(processor_brand)) from sales.sp;

select std(screen_size) from sales.sp;

select variance(screen_size) from sales.sp;

select ceil(screen_size) from sales.sp;

select floor(screen_size) from sales.sp;


create database sales;

select model, screen_size from sales.sp 
where brand_name = "samsung"
order by screen_size DESC
limit 1;

select model, num_front_cameras + num_rear_cameras as total 
from sales.sp
order by total desc;

select model,
round(sqrt(resolution_width*resolution_width+
resolution_height*resolution_height)/screen_size) as ppi
from sales.sp 
order by ppi desc;

SELECT model, battery_capacity
from  sales.sp
ORDER BY battery_capacity desc limit 1,1;

-- find 2nd largest 
SELECT model, battery_capacity
from  sales.sp
ORDER BY battery_capacity desc limit 3,2;

-- find worst apple phone
select model, rating
from sales.sp
where brand_name = "apple"
order by rating asc limit 1;

-- find low to high price 
select * from sales.sp
order by brand_name asc, price asc;   

select * from sales.sp
order by brand_name asc, rating asc;

-- Group by
-- brand name with smartphones
select brand_name, count(*) as "count", 
round(avg(price),2) as "avg_price",
round(avg(screen_size),2) as "screen_size"
from sales.sp
group by brand_name
order by count desc limit 5;

-- group smartphone whether nfc 
select has_nfc, avg(price) as "avg_price",
avg(rating) as "rating"
from sales.sp
group by has_nfc; 


select has_5g, avg(price) as "avg_price",
avg(rating) as "rating"
from sales.sp
group by has_5g;



select fast_charging, avg(price) as "avg_price",
avg(rating) as "rating"
from sales.sp
group by fast_charging;


```
