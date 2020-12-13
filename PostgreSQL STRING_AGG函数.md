#### PostgreSQL STRING_AGG函数

1.目的：根据分组，拼接某一字段

~~~ sql
SELECT
	string_agg ( tn_tesk_item_value, '、' ORDER BY r.createtime ) AS rs 
FROM
	task_item_record AS r 
WHERE
	to_char( r.createtime, 'yyyy-MM-dd' ) = '2020-12-11' 
	AND r.platstatus = 1
~~~

可以用distinct，group by

