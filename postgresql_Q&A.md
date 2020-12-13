### postgresql

Select first row in each GROUP BY group?
WITH summary AS (
    SELECT p.id, 
           p.customer, 
           p.total, 
           ROW_NUMBER() OVER(PARTITION BY p.customer 
                                 ORDER BY p.total DESC) AS rk
      FROM PURCHASES p)
SELECT s.*
  FROM summary s
 WHERE s.rk = 1

