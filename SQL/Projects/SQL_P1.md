
```
use sql_p1;
SELECT * FROM sales;

select * from sales limit 10;

select count(transactions_id) from sales;

SELECT *
FROM sales
WHERE transactions_id = 1225;

-- total sales
select sum(total_sale) from sales;

-- total customer 
select count( distinct customer_id) from sales;
  
-- unique category
select count(distinct category) from sales;

DESCribe sales;

-- sales on 2022-11-05
SELECT *
FROM sales
WHERE date(sales_date) = '2022-11-05';

-- clothing with qty > 1
SELECT *
FROM sales
WHERE category = 'clothing'
  AND DATE_FORMAT(sale_date, '%Y-%m') = '2022-11' and quantiy = 4;
  
-- total sales for each category
select category, sum(total_sale) from sales
GROUP BY category;

-- avg age of customer category wise
select category, round(avg(age),2) from sales
group by category;

-- total sales greater than 1000
select * from sales
where total_sale > 1000;

-- total transaction by gender and category 
select category, gender, count(*) as total_trans
from sales
group by category, gender
order by 1;

-- calculate average sales for each month find out best selling month each year
select * from 
(select year(sale_date) as year, month(sale_date) as month, round(avg(total_sale),2),
rank() over(partition by year(sale_date) order by round(avg(total_sale),2) desc) as ranks
from sales
GROUP BY 1,2) as t1
where ranks = 1;

-- find top 5 customer based on the highest total sales
 select customer_id, sum(total_sale)
 from sales
 group by 1
 order by 2 desc
 limit 5;
 
-- find unique customer who purchased item from each category
select category, count(distinct customer_id) 
from sales
group by category;

-- create morning, evening , night shift - no. of order
with hourly_sales as
(select *,
case
	when hour(sale_time) < 12 then "Morning"
	when hour(sale_time) between 12 and 17 then "Afternoon"
Else "Evening" end as shift
from sales)
select shift, count(*) from hourly_sales
group by shift;

```
