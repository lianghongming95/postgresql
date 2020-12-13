### postgresql 自定义函数

1. 无入参有返回

```plsql
create or REPLACE FUNCTION lhm_test_fun()
returns integer as $total$

declare total int;
begin
select count(*) into total from pl_orgstruct;
RETURN total;
end
$total$ LANGUAGE plpgsql;
select lhm_test_fun();
```

2. 有入参有返回

   ```plsql
   CREATE OR REPLACE FUNCTION "public"."lhm_test_fun_inandout"("orgname" varchar)
     RETURNS "pg_catalog"."int4" AS $BODY$
   DECLARE 
    rental_duration INTEGER; 
   BEGIN
   
    SELECT count(*)  INTO rental_duration 
       FROM pl_orgstruct a
    WHERE a.orgname like '%' || orgname ||'%';
    RETURN rental_duration;
   END; $BODY$
     LANGUAGE plpgsql VOLATILE
     COST 100
   ```

   

3. 没入参返回一个表

   ```plsql
   create or replace function f_get_lhm_test_fun_returnquery() 
   returns setof pl_orgstruct 
   as 
   $$
   select * from pl_orgstruct;
   $$
   language 'sql';
   ```

   

