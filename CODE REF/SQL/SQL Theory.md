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

## Title
```c#
/*
	>  
 *
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```

## Title
```c#
/*
	> 
*
```
