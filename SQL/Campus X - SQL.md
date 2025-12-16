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
