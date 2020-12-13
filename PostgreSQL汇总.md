### PostgreSQL汇总rollup

#### rollup适合用算报表合计和小计

~~~ sql
DROP TABLE IF EXISTS sales_test;
CREATE TABLE sales_test (
    brand VARCHAR NOT NULL,
    segment VARCHAR NOT NULL,
    quantity INT NOT NULL,
    PRIMARY KEY (brand, segment)
);


INSERT INTO sales_test (brand, segment, quantity)
VALUES
    ('ABC', 'Premium', 100),
    ('ABC', 'Basic', 200),
    ('XYZ', 'Premium', 100),
    ('XYZ', 'Basic', 300);
		
		
		SELECT
    brand,
    segment,
    SUM (quantity)
FROM
    sales_test
GROUP BY
    ROLLUP (brand, segment)
		ORDER BY
    brand,
    segment;
~~~

