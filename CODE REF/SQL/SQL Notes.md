

# =// Basics //=

## SELECT

````sql
SELECT column_1, column_2 FROM table_A;
````

## DISTINCT (Unique)

```sql
SELECT DISTINCT(colour) FROM table_of_colours; [[returns]] column of unique values, i.e. red, green, blue

SELECT DISTINCT(rating) FROM film; [[show]] all the unique ratings available.
```

## COUNT

```sql
SELECT COUNT(customer_id) FROM customer; [[returns]] the number of rows with customer_id.

SELECT COUNT(DISTINCT(payment)) FROM customer; [[retuns]] the number of rows of unique payments.
```

## WHERE

```sql
SELECT * FROM film WHERE price >= 10 AND price <= 20; [[filtering]]
SELECT email FROM customer WHERE first_name = 'Nancy' AND last_name = 'Thomas'
```

## ORDER BY

````sql
# order by store_id first, then order by the first name. 
SELECT first_name,last_name,store_id FROM customer ORDER BY store_id ASC, first_name ASC
````

## LIMIT

```sql
# Limit the number of rows returned.
SELECT * FROM customer WHERE payments > 0.00 LIMIT 5; [[return]] 5 rows where payment is > 0.

SELECT * FROM payment ORDER BY payment_date ASC LIMIT 10;
```

## BETWEEN

```sql
[[BETWEEN]] is inclusive so, >= <=. when using NOT BETWEEN its > <
SELECT * FROM customer WHERE payment BETWEEN 1 AND 9; # payments between 1 and 9.
```

## IN

````sql
# use IN when returning multiple rows of results rather then WHERE
SELECT * FROM colour_table WHERE color IN ('red', 'green'); [[if]] color column have a value of 'red' or 'green', then return that row.

SELECT * FROM colour_table WHERE color NOT IN ('red', 'green'); [[retuns]] rows where colours  are not red or green.
````

## LIKE

````sql
# LIKE is case-sensitive and ILIKE is not.
# %: any number of characters before or after, i.e. %car%.
# _: single character. i.e. _car_ or car__ or car___.
SELECT * FROM customer WHERE f_name LIKE 'J%'; 
SELECT * FROM customer WHERE f_name ILIKE 'J%'; 
````

## Functions

```sql
[[basic]] functions are
# COUNT()
# AVG()
SELECT AVG(replacement_cost) FROM film;
SELECT ROUND(AVG(replacement_cost),2) FROM film; [[rounds]] to 2 decimal points.

# MIN()/MAX()
SELECT MIN(replacement_cost) FROM film;

# SUM()
SELECT SUM(replacement_cost) FROM film;
```

# =// Intermediate //=

## GROUP BY

![[Screenshot from 2021-09-12 09-23-48.png]]

```sql
# Only comes after FROM ar WHERE statement.
# used to categorize a column.

# most paid customers 
SELECT customer_id, SUM(amount) FROM payment [[add]] all payments with the same customer id
GROUP BY (customer_id) # categorise by customer-id
ORDER BY SUM(amount) DESC # have to use SUM(payment) to do order by
```

````sql
# groupi by more than one column
SELECT staff_id, customer_id, SUM(amount) FROM payment
GROUP BY (staff_id, customer_id) 
ORDER BY staff_id, customer_id  # categorize by customer store id 1st, then customer-id
````

![[Screenshot from 2021-09-12 14-34-29.png]]



```sql
# top 5 paying customers to send coupons
SELECT customer_id, SUM(amount_paid) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5
```

## HAVING

```sql
# HAVING can be used after GROUP BY for additional filter
SELECT company, SUM(sales) FROM finance_tbl
GROUP BY company
HAVING SUM(sales) > 3000

# Having is similar to WHERE but can be used after SUM(sales) is done executing

# Platinum status for customers with 40 or more transactions
SELECT customer_id, COUNT(*) FROM payment
GROUP BY customer_id
HAVING COUNT(amount)>= 40
ORDER BY COUNT(amount) DESC
```

## AS

```sql
# Used to give an alias to a column.
SELECT COUNT(amount) AS num_transactions FROM payment;
```

## JOINS

```sql
# Joins allow us to combine tables.
```

### INNER JOIN

```sql
# Used for when match in both tables.
# Just using JOIN defaults to INNER JOIN
```

![[Screenshot from 2021-09-14 09-29-42.png]]

```sql
# Join customer & payment tables with customer id.
# tbl_name.col_name
SELECT payment.customer_id, payment.payment_id, customer.first_name FROM payment
INNER JOIN customer ON customer.customer_id = payment.customer_id;


# All the movies 'Nick Wahlberg' is in.
SELECT actor.first_name, actor.last_name, film_actor.film_id, film.title FROM actor
INNER JOIN film_actor ON film_actor.actor_id = actor.actor_id
INNER JOIN film ON film_actor.film_id = film.film_id
WHERE actor.first_name = 'Nick' AND actor.last_name = 'Wahlberg'
```

### FULL OUTER JOIN

```sql
# Joins everything if it doesn't match

SELECT customer.address_id, address.address_id, customer.first_name, customer.last_name, customer.email, address.district FROM customer
FULL OUTER JOIN address ON customer.address_id = address.address_id
WHERE address.district = 'California'
ORDER BY customer.customer_id, address.address_id ASC
```

![[Screenshot from 2021-09-14 09-57-56.png]]

```sql
# Return null where it doesn't have a value present.
# We can use the nulls to do additional filtering with the WHERE clause
```

![[Screenshot from 2021-09-14 09-59-45.png]]
```sql
# Checks if there are any customer details are present in DB where they have never made any payments.

SELECT * FROM customer
FULL OUTER JOIN payment ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS NULL OR payment.customer_id IS NULL
```

### LEFT JOIN

```sql
# Everything in table A & table A & B.
# A U (A N B)
```

![[Screenshot from 2021-09-14 10-27-19.png]]


![[Screenshot from 2021-09-14 10-29-10.png]]

```sql
# Again we can perform an adition filter on the null values.
SELECT * FROM Registrations 
LEFT JOIN Logins ON Registrations.name = Logins.name # LEFT OUTER JOIN is same as LEFT JOIN
WHERE Registrations.name IS NULL OR Logins.name IS NULL
```

### RIGHT JOIN

```sql
# Opposite of a Left Join. 
# B U (A N B)
# you can JUST USE LEFT JOIN by ordering the tables in a different order.
```

![[Screenshot from 2021-09-15 09-52-10.png]]

### UNION

```sql
# Copy and paste 2 SELECT statements

SELECT * FROM customer
UNION
SELECT * FROM vip_customer;
```

![[Screenshot from 2021-09-15 10-01-32.png]]

![[Screenshot from 2021-09-15 10-01-50.png]]



# =// Advanced //=

## SHOW

```sql
# Show all the settings
SHOW ALL;
```
## Time and Date

![[Screenshot from 2021-09-18 08-15-49.png]]

```sql
# you can always remove time from TIMESTAMP or zone from TIMESTAMPZ but you cant add them back in. 
```



### Time/Date Functions

![[Screenshot from 2021-09-18 08-22-15.png]]

```sql
# Show current set timezone
SHOW TIMEZONE;
```

```sql
# Returns current timestamp info.
SELECT NOW();

# REturns in a string, more readable.
SELECT TIMEOFDAY;
```

### Time/Date Formatting

```sql
[[to]] remove timestamp from a date-and-time combination use DTAE()
SELECT DATE(payment_date) FROM payment; [[returns]] just date without timestamp.
```

```sql
# functions used to format
```

![[Screenshot from 2021-09-18 08-33-15.png]]




![[Screenshot from 2021-09-18 08-34-47.png]]



```sql
# EXTRACT(YEAR FROM date_col), it can be 
# -YEAR
# -MONTH
# -DAY
# -WEEK
# -QUARTER
# -dow   day of the week

SELECT EXTRACT(YEAR FROM payment_date) FROM payment;
SELECT EXTRACT(QAUARTER FROM payment_date) FROM payment;
```

```sql
# AGE(date_col), returns how old the date is compared to the current date.

SELECT AGE(payment_date) FROM payment;
```

```sql
# Returns text
# TO_CHAR(date_col, 'dd-mm-yyyy')

SELECT TO_CHAR(payment_date, 'dd-mm-yyyy') FROM payment;

# see more TO_CHAR() use cases.
```



## MATHEMATICAL Functions

<img src="E:\docs\CODE REF\img\Screenshot 2021-11-24 125732.png" alt="Screenshot 2021-11-24 125732" style="zoom: 150%;" />

### Docs link: 

 [PostgreSQL Math Functions.html](img\PostgreSQL Math Functions.html) 

## STRING Functions

<img src="E:\docs\CODE REF\img\Screenshot 2021-11-24 130158.png" alt="Screenshot 2021-11-24 130158" style="zoom:150%;" />

```sql
# concatinate two collums and add a space between them.
# ' ' are string quotes, so u can have anything. i.e '--' or '/'
SELECT first_name || ' ' || last_name
FROM customer as fullName;


# LEFT returns the n characters from the left. i.e LEFT(sammuel, 3) = sam
SELECT LOWER(LEFT(first_name,1)) || LOWER(last_name) || '@gmail.com'
AS customer_email
FROM customer;
```

## Docs link: 

 [PostgreSQL_ Documentation_ 9.1_ String Functions and Operators.html](img\PostgreSQL_ Documentation_ 9.1_ String Functions and Operators.html) 

## SUB QUERIES

```sql
#[[sub]] queries allow you to perform additional queries of a result of another query.
#[[try]] executing subquery 1st to see if it yields any result, then use that result to perform additional queries.

SELECT student, grade
FROM test_scores
WHERE grade > (SELECT AVG(grade) FROM test_scores); [[inside]] the perenthesis is the subquery
```



## SELF JOINS

```sql
#[[self]] join is a joining table to itself.
#[[You]] must use aliases for tables when using self joins.

SELECT tableA.col, tableB.col
FROM table AS tableA
JOIN table AS tableB ON
tableA.some_col = tableB.other_col;
```



```sql
[[Each]] employee sends a reports to anorther employee
```

![[Screenshot 2021-12-09 162618.png]]

```sql
SELECT emp.name, report.name AS rep
FROM employees AS emp
JOIN employees AS report ON
emp.emp_id = report.report_id;
```





# =//Cheatsheet//=
![[Screen+Shot+2016-04-17+at+12.22.49+PM (1).png]]
