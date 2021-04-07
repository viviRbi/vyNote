```sql
SELECT * FROM `employee` ORDER BY `salary` DESC LIMIT 1 OFFSET 2;


-- Offset 2, limit 1. Best solution
SELECT DISTINCT salary FROM employee ORDER BY salary DESC LIMIT 2, 1;


SELECT TOP 1 salary 
FROM 
    (SELECT TOP 3 salary 
     FROM Table_Name 
     ORDER BY salary DESC) AS Comp 
ORDER BY salary ASC
```