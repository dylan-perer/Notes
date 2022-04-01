## What is RDBMS and SQL
```c#
/*
	> RDBMS is a collection of realated tables.
	> SQL is a query languege where we can execute querys on tables.
*
```

## Explain normalization
```c#
/*
	> Its a design technique to remove redudant data.
*
```

## How is normalization implemented?
```c#
/*
	> We split the tables intto refernce and transaction tables.
*
```

## What is denormalization.
```c#
/*
	> It is a design technique to improve search performance.
*
```

## How is denormalization implemented?
```c#
/*
	> We merge tables.
*
```

## Explain Online transaction processing(OLTP) vs Online analytical processing (OLAP)
```c#
/*
	> In order to balance data redudancy and serach performance we create 2 databases, OLTP database which focuses on normalization/avoiding data redudancy and OLAP which focuses on denomalization/search perofomance
*
```

## Explain 1st, 2nd, 3rd normal form (A.P.T)
```c#
/*
	> A.P.T, columns must be atomic, no partial depedencies, no transient depedencies.
		- 1st normal form is achieved when all columns in a table has atomic values.
		- 2nd normal form is achieved when 1st normal form is achived and all non key columns are fully dependant on the primary key.
		- 3rd normal form is achived when 1st and 2nd normal form are achived and no transient dependecy should be present.
*
```

## Primary key vs Unique key
```c#
/*
	> They both uniquely identifies a row on a table but primary key cannot be set null.
	> Also table can have only one primary key.
*
```

## Char vs Varchar?
```c#
/*
	> Char is fixed length. it will always take the pre-defined memory size.
	> Varchar can also be fixed length, however memoery size will vary depending on the value.
*
```

## nchar vs char?
```c#
/*
	> nchar can store non english characters.
*
```

## Explain indexing
```c#
/*
	> Indexes are used to increase serach performance.
	> Created a b-tree.
	> Its similar to a index on a book.
*
```

## Explain Clustered vs non clustered index
```c#
/*
	> In clsutered index, leaf node will point to the actual data. (there can only be 1 on table)
	> Non clustered index, leaf node will point to a clustred index. (you can have many on a table)
*
```

## Explain Functions vs Store Procedures
```c#
/*
	> Function are used to compute values, they cannot make permanent changes.
	> Stored procedures are mini programs that can manipulate database.
*
```

## What are triggers?
```c#
/*
	> It is some logic that can be executed on events like insert, update or delete.
*
```

## What is a transaction
```c#
/*
	> Transaction allows us to combine multiple queries and exceuted them as a single query.
	> Either all will execute successfully or fail and rolled back.
*
```

## Explain inner joins
```c#
/*
	> Inner joins join two tables with a common coulmn.
*
```

## Explain left joins
```c#
/*
	> Everything on left table is selected and joined with right table wether there is a value present or not.
*
```

## Explain right joins
```c#
/*
	> Everything on right table is selected and joined with left table wether there is a value present or not.
*
```

## Explain full outer join
```c#
/*
	> Combination of left and right join. All matching and unmatching records from both left and right tables are selected.
*
```

## Explain cross joins
```c#
/*
	> Every record of one table is join with other table records.
*
```

## Explain union
```c#
/*
	>   Combines two tables togather into one table.
 *
```

## Can union be perfomed on tables with different numbe of columns?
```c#
/*
	> No.
*
```

## Can union be perfomed on tables with different data types?
```c#
/*
	> No, column datatype has to be the same.
*
```

## What are some aggreagte functions you have used?
```c#
/*
	> AVG()
	> COUNT()
	> MIN()
	> MAX()
*
```

## Explain group by
```c#
/*
	> It convers rows into summary rows using a common values.
*
```

## Can we group by on a column that is not on the select statement?
```c#
/*
	> No, select statement must have th column that you are going to do a group by.
*
```

## What is having clause?
```c#
/*
	> It allows you to filter after a group by.
*
```

## Explain difference between Where vs Having clause
```c#
/*
	> Where is executed before a group by, and cannot have aggregate function.
	> Having is executed after a group by, and can have aggregate function.
*
```

## How can we sort in sql?
```c#
/*
	> Usinng order by, default is asc.
*
```

## How to select only unique values?
```c#
/*
	> Using distinct keyword.
*
```

## How to limit sql query results
```c#
/*
	> Using limits in mysql or using top(x) is ms sql server
*
```

## What are wild cards?
```c#
/*
	> It allows you to do string pattern matching(LIKE/ILIKE).
*
```

## What are case statement?
```c#
/*
	> When a condition is met show the case then statement on the column. i.e. if money spent is greater that $700 in a colmun show a message as
	high spender.
*
```

## What is self reference table
```c#
/*
	> When a table's primary key is refered in it's table (PK and FK are in the same table).
*
```

## Explain self join
```c#
/*
	> Similar to a inner join, but it joins a table with it self.
*
```

## Explain between clause
```c#
/*
	> Allows you to find values using a range.
*
```

## Explain sub-query
```c#
/*
	> Query inside another query.
*
```

## Can inner subquery return mutiple values?
```c#
/*
	> Yes, but you must use IN clause rather than =.
*
```

## What a co-related query?
```c#
/*
	> similar to sub query but gets executed row by row.
*
```

