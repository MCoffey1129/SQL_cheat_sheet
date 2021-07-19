SQL cheat sheet
===

Investigate the contents of a table
---

* Quickly see the contents of table_1 in Lab_A 
~~~~sql
help TABLE Lab_A.Table_1
~~~~

Investigate the code behind a view
---

* Quickly see the code behind vw_1 in Lab_A
~~~~sql
show VIEW Lab_A.vw_1
~~~~


Volatile tables
---

***CREATE TABLE***  
~~~~sql
CREATE VOLATILE TABLE temp
(
Column_A VARCHAR(20)
)ON COMMIT PRESERVE ROWS; 
~~~~

***INSERT VALUES***
~~~~sql
INSERT INTO temp sel column_A from LAB_A.Table_A;
~~~~

***QUERY TABLE TO CONFIRM VALUES***
~~~~sql
sel * from temp
~~~~

Duplication check
---
~~~~sql
select column_B, count(column_B) as cnt_B
from Table_B
group by column_B 
having count(column_B) > 1
~~~~

Querying the DBC
---

* Check what tables in Lab_A contain a column with the word "salary" in their name 
~~~~sql
select * from dbc.columns
where columnname like '%salary%'
and databasename = 'LAB_A'
~~~~

* Check what tables in Lab_A contain the word "salary" in their name 
~~~~sql
select * from dbc.columns
where columnname like '%salary%'
and databasename = 'LAB_A'
~~~~

Declaring a variable 
---

* Declare a variable "counter" as 20 (defined as an integer), insert a while loop increasing the counter by 1 at each iteration until it hits 30 

~~~~sql
DECLARE @counter INT
SET @counter = 20

while @counter < 30

Begin 
  select @counter = @counter + 1
 end
 
 select @counter
~~~~


Rank and partition
---

* Get the latest salary record for each customer 
~~~~sql
select customer, salary
from Table_A
qualify RANK() OVER (partition by customer order by dt_time) = 1 
~~~~

* Window function   
~~~~sql
select OrderID, location,
count(location)
over(Partition by location) as TotalOrders
from Orders
~~~~


* Use Lead() and Lag() to get the previous and next value in a window
~~~~sql
select location, order_date
LAG(order_date)
over(Partition by location order by order_date) as Previousorder
Lead(order_date)
over(Partition by location order by order_date) as Nextorder
from Orders
~~~~

* Running total
~~~~sql
select location, order_date
sum(price)
over(Partition by location order by order_date) as location_total
from Orders
~~~~


