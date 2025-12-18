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

 
