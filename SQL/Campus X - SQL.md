Campus X Playlist - https://www.youtube.com/watch?v=CTLwYjh92xw&list=PLBv9GORP5VkclmbvgNaEB3GBFc-weefX7

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

