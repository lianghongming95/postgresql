### PostgreSQL ROW_NUMBER函数

#### 作用：根据某一字段分组排序,也可以不进行分组

~~~ sql
CREATE TABLE product_groups_test (
	group_id serial PRIMARY KEY,
	group_name VARCHAR (255) NOT NULL
);



CREATE TABLE products_test (
	product_id serial PRIMARY KEY,
	product_name VARCHAR (255) NOT NULL,
	price DECIMAL (11, 2),
	group_id INT NOT NULL,
	FOREIGN KEY (group_id) REFERENCES product_groups_test (group_id)
);


INSERT INTO product_groups_test (group_name)
VALUES
	('Smartphone'),
	('Laptop'),
	('Tablet');
	
	
	
	
	INSERT INTO products_test (product_name, group_id,price)
VALUES
	('Microsoft Lumia', 1, 200),
	('HTC One', 1, 400),
	('Nexus', 1, 500),
	('iPhone', 1, 900),
	('HP Elite', 2, 1200),
	('Lenovo Thinkpad', 2, 700),
	('Sony VAIO', 2, 700),
	('Dell Vostro', 2, 800),
	('iPad', 3, 700),
	('Kindle Fire', 3, 150),
	('Samsung Galaxy Tab', 3, 200);
	
	

	
	SELECT
	product_id,
	product_name,
	group_id,
	ROW_NUMBER () OVER (PARTITION BY group_id ORDER BY product_name)
FROM
	products_test;
~~~

