**Joines**

Joins in SQL are used to combine data from two or more tables using a common column.

Simple meaning - When data is split into different tables, JOIN helps you see it together.

Why joins are needed - 

Example:

One table has customer details

Another table has orders

To see who ordered what, we use JOIN.

Main types of JOINs -

1. INNER JOIN
   
Gives only matching records from both tables

<img width="231" height="158" alt="img_inner_join" src="https://github.com/user-attachments/assets/9b7125b3-bd65-466f-8bd3-a8be64d1136d" />

```
SELECT *
FROM customers c
INNER JOIN orders o
ON c.cid = o.cid;
```

