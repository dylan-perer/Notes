## Create table
```sql server
CREATE TABLE product(
	id INT PRIMARY KEY,
	name VARCHAR(20) NOT NULL,
	display_order INT,
	created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP 
);
```

