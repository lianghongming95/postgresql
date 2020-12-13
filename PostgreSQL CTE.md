#### PostgreSQL CTE

#### 目的：简化查询

1. 查询

   ​										

   ~~~mysql
   WITH regional_sales AS (
           SELECT customercode, SUM(amount) AS total_sales
           FROM kx_order
           GROUP BY customercode
        ), top_regions AS (
           SELECT customercode
           FROM regional_sales
           WHERE total_sales > (SELECT SUM(total_sales)/10 FROM regional_sales)
        )
   SELECT customercode,
   				salesmanid,
   				ordertime,
          SUM(amount) AS product_sales
   FROM kx_order
   WHERE customercode IN (SELECT customercode FROM top_regions)
   GROUP BY customercode,salesmanid,ordertime
   ~~~

   ~~~plsql
   WITH table_1 AS (
   SELECT GENERATE_SERIES('2012-06-29', '2012-07-03', '1 day'::INTERVAL) AS date
   )
   
   , table_2 AS (
   SELECT GENERATE_SERIES('2012-06-30', '2012-07-13', '1 day'::INTERVAL) AS date
   )
   
   SELECT * 
   FROM
        table_1 t1
        INNER JOIN 
        table_2 t2
        ON t1.date = t2.date
   ;
   ~~~

   

2. 更新todo

3. 迭代

   ~~~sql
   WITH RECURSIVE _r AS (
   	SELECT
   		_s.saleorgid AS orgstructid 
   	FROM
   		pl_saleorg_resp _s 
   	WHERE
   		_s.platstatus = 1 
   		AND _s.memberid = '1323832399565557760' UNION ALL
   	SELECT
   		_a.orgstructid 
   	FROM
   		pl_orgstruct _a
   		INNER JOIN pl_orgtype _t ON _a.orgtypeid = _t.orgtypeid 
   		AND _t.orgtypecategory = 1,
   		_r 
   	WHERE
   		_a.parentorgstructid = _r.orgstructid 
   	) SELECT
   	orgstructid 
   FROM
   	_r
   ~~~

   

