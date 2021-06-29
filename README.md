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

* Check every table in LAB_A for a column containing the word salary
~~~~sql
select * from dbc.columns
where columnname like '%salary%'
and databasename = 'LAB_A'
~~~~

* Check every table containing the word salary in Lab_A
~~~~sql
select * from dbc.columns
where columnname like '%salary%'
and databasename = 'LAB_A'
~~~~

Rank and partition
---

* Get the latest salary record for each customer 
~~~~sql
select customer, salary
from Table_A
qualify RANK() OVER (partition by customer order by dt_time) = 1 
~~~~


