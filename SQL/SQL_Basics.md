___
# Structured Query Language (SQL) 
</br>
# Entity Relationship Diagrams
An entity relationship diagram (ERD) is a common way to view data in a database. Below is the ERD for the database we will use from Parch & Posey. These diagrams help you visualize the data you are analyzing including:

1. The names of the tables.
2. The columns in each table.
3. The way the tables work together.

![tables with data](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/59821d7d_screen-shot-2017-08-02-at-11.14.25-am/screen-shot-2017-08-02-at-11.14.25-am.png)

</br>

# Why Businesses Like Databases
1. Data integrity is ensured

2. Data can be accessed quickly

3. Data is easily shared

</br>

# A few key points about data stored in SQL databases:

1. Data in databases is stored in tables that can be thought of just like Excel spreadsheets.

2. All the data in the same column must match in terms of data type. This can be very bad if you want to do math with this column!

3. Consistent column types are one of the main reasons working with databases is fast.

</br>

# SQL Statements

1. `CREATE TABLE` is a statement that creates a new table in a database.
2. `DROP TABLE` is a statement that removes a table in a database.
3. `SELECT` allows you to read data and display it. This is called a query.

The `SELECT` statement is the common statement used by analysts, and you will be learning all about them throughout this course!


```SQL
SELECT *
    FROM demo.orders
```
`SELECT` is where you tell the query what columns you want back.

`FROM` is where you tell the query what table you are querying from. Notice the columns need to exist in this table.

</br>

# Use White Space in Queries
```SQL
 SELECT account_id FROM orders
is equivalent to this query:
```
```SQL
SELECT account_id
FROM orders
```

# SQL isn't Case Sensitive
```SQL
SELECT account_id
FROM orders
is the same as:
```
```SQL
select account_id
from orders
```

# Semicolons

**Best practice:**
```SQL
SELECT account_id
FROM orders;
```
</br>
</br>

_______
# LIMIT
The `LIMIT` command is always the very last part of a query. An example of showing just the first 10 rows of the orders table with all of the columns might look like the following:
```SQL
SELECT *
    FROM orders
    LIMIT 10;
```

</br>

# ORDER BY

The `ORDER BY` statement allows us to order our table by any row. 
The `ORDER BY` statement is always after the `SELECT` and `FROM` statements, but it is before the `LIMIT` statement. 

```SQL
SELECT *
    FROM orders
  ORDER BY occured_at
  LIMIT 10;
```


Pro Tip
Remember `DESC` can be added after the column in your ORDER BY statement to sort in descending order, as the default is to sort in ascending order.

Examples

```SQL
SELECT id, occurred_at, total_amt_usd
    FROM orders
  ORDER BY occurred_at
  LIMIT 10;

SELECT id, account_id, total_amt_usd
    FROM orders
  ORDER BY total_amt_usd DESC
  LIMIT 5;
  
SELECT id, account_id, total
    FROM orders
  ORDER BY total
  LIMIT 20;

/* returns the top 5 rows from orders ordered according to newest to oldest, but with the largest total_amt_usd for each date listed first for each date */

SELECT occurred_at, total_amt_usd
    FROM orders
  ORDER BY occurred_at, total_amt_usd DESC
  LIMIT 5;

/* returns the top 10 rows from orders ordered according to oldest to newest, but with the smallest total_amt_usd for each date listed first for each date. */
  
SELECT occurred_at, total_amt_usd
    FROM orders
  ORDER BY occurred_at DESC, total_amt_usd
  LIMIT 10;
```

</br>

# WHERE
Using the `WHERE` statement, we can subset out tables based on conditions that must be met.

Common symbols used within WHERE statements include:

1. `>` (greater than)

2. `<` (less than)

3. `>=` (greater than or equal to)

4. `<=` (less than or equal to)

5. `=` (equal to)

6. `!=` (not equal to)

```SQL
SELECT *
    FROM orders
  WHERE account_id = 4251
  ORDER BY occured_at
  LIMIT 10;

/* Pull the first 5 rows and all columns from the orders table that have a dollar amount of gloss_amt_usd greater than or equal to 1000. */
SELECT *
    FROM orders
  WHERE gloss_amt_usd >= 1000
  LIMIT 5;

/* Pull the first 10 rows and all columns from the orders table that have a total_amt_usd less than 500. */
SELECT *
    FROM orders
  WHERE total_amt_usd < 500
  LIMIT 10;

/* The WHERE statement can also be used with non-numerical data. We can use the = and != operators here. */
SELECT *
    FROM orders
  WHERE name != 'Kelly'
  LIMIT 10;

/* Filter the accounts table to include the company name, website, and the primary point of contact (primary_poc) for Exxon Mobil in the accounts table. */
SELECT name, website, primary_poc
    FROM accounts
  WHERE name = 'Exxon Mobil'
```

</br>

# Derived Columns
Creating a new column that is a combination of existing columns is known as a derived column.

Common operators include:
1. `*` (Multiplication)
2. `+` (Addition)
3. `-` (Subtraction)
4. `/` (Division)

```SQL
SELECT completed_orders,
    pre_orders,
    completed_orders + pre_orders AS total_orders
    FROM orders
  ORDER BY total_orders
  LIMIT 10;

/* Create a column that divides the standard_amt_usd by the standard_qty to find the unit price for standard paper for each order. Limit the results to the first 10 orders, and include the id and account_id fields. */

SELECT id, 
	account_id,
	standard_amt_usd / standard_qty AS standard_paper
    FROM orders
  LIMIT 10;
  
/* Write a query that finds the percentage of revenue that comes from poster paper for each order. You will need to use only the columns that end with _usd. (Try to do this without using the total column). Include the id and account_id fields. */

SELECT id, 
	account_id,
	poster_amt_usd / (standard_amt_usd + gloss_amt_usd + poster_amt_usd) AS post_rev_per
    FROM orders
    WHERE id like '%_usd';
```

</br>

# Logical Operators

1. `LIKE`

    This allows you to perform operations similar to using WHERE and =, but for cases when you might not know exactly what you are looking for. 

    ```SQL
    /* ends with _usd */
    WHERE id like '%_usd'

    /* has _usd anywhere */
    WHERE id like '%_usd%'
    
    /* All the companies whose names start with 'C'. */

    SELECT 
        FROM accounts
    WHERE name LIKE 'C%';

    /* All companies whose names contain the string 'one' somewhere in the name. */
    SELECT 
        FROM accounts
    WHERE name LIKE '%one%';
    
    /* All companies whose names end with 's'. */
    SELECT 
        FROM accounts
    WHERE name LIKE '%s';

    ```

2. `IN`

    This allows you to perform operations similar to using WHERE and =, but for more than one condition.
    
    ```SQL
    /* accounts in Walmart and Apple */
    SELECT 
        FROM accounts
    WHERE name IN ('Walmart', 'Apple');

    /* accounts in 1000 and 1201 */
    SELECT 
        FROM accounts
    WHERE account_id IN (1000, 1201);

    /*Use the accounts table to find the account name, primary_poc, and sales_rep_id for Walmart, Target, and Nordstrom. */
    SELECT name, primary_poc, sales_rep_id
        FROM accounts
    WHERE name IN ('Walmart', 'Target', 'Nordstrom');
    
    /*Use the web_events table to find all information regarding individuals who were contacted via the channel of organic or adwords. */
    SELECT *
        FROM web_events
    WHERE channel IN ('organic', 'adwords')
    ```


3. `NOT`

    This is used with IN and LIKE to select all of the rows NOT LIKE or NOT IN a certain condition. By specifying NOT LIKE or NOT IN, we can grab all of the rows that do not meet a particular criteria.

    ```SQL
    /*Use the accounts table to find the account name, primary poc, and sales rep id for all stores except Walmart, Target, and Nordstrom.*/
    SELECT name, primary_poc, sales_rep_id
        FROM accounts
    WHERE name NOT IN ('Walmart', 'Target', 'Nordstrom');
    
    /*Use the web_events table to find all information regarding individuals who were contacted via any method except using organic or adwords methods.*/
    SELECT *
        FROM web_events
    WHERE channel NOT IN ('organic', 'adwords');

    /*All the companies whose names do not start with 'C'.*/
    SELECT name
        FROM accounts
    WHERE name NOT LIKE 'C%';

    /*All companies whose names do not contain the string 'one' somewhere in the name.*/
    SELECT name
        FROM accounts
    WHERE name NOT LIKE '%one%';

        
    /*All companies whose names do not end with 's'.*/
    SELECT name
        FROM accounts
    WHERE name NOT LIKE '%s';
    ```

4. `AND & BETWEEN`

    These allow you to combine operations where all combined conditions must be true. 

     `LIKE`, `IN`, and `NOT` logic can also be linked together using the `AND` operator.

    Sometimes we can make a cleaner statement using BETWEEN than we can using AND. 

    Instead of writing :
    ```SQL
    WHERE column >= 6 AND column <= 10
    ```
    we can instead write, equivalently:
    ```SQL
    WHERE column BETWEEN 6 AND 10
    ```

    ```SQL
    /*Write a query that returns all the orders where the standard_qty is over 1000, the poster_qty is 0, and the gloss_qty is 0.*/
    SELECT standard_qty, poster_qty, gloss_qty
        FROM orders
    WHERE standard_qty > 1000 AND poster_qty = 0 AND gloss_qty = 0;

    /*Using the accounts table find all the companies whose names do not start with 'C' and end with 's'.*/
    SELECT name
        FROM accounts
    WHERE name NOT LIKE 'C%' AND name NOT LIKE '%s';
    
    /*Use the web_events table to find all information regarding individuals who were contacted via organic or adwords and started their account at any point in 2016 sorted from newest to oldest.*/
    SELECT *
        FROM web_events
    WHERE channel IN ('organic', 'adwords') AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
    ORDER BY occurred_at DESC;
    ```


5. `OR`

    This allow you to combine operations where at least one of the combined conditions must be true.
    This operator works with all of the operations we have seen so far including arithmetic operators (+, *, -, /), `LIKE`, `IN`, `NOT`, `AND`, and `BETWEEN` logic can all be linked together using the `OR` operator.

    ```SQL
    /*Find list of orders ids where either gloss_qty or poster_qty is greater than 4000. Only include the id field in the resulting table.*/
    SELECT id
        FROM orders
    WHERE poster_qty > 4000 OR gloss_qty > 4000;
    
    /*Write a query that returns a list of orders where the standard_qty is zero and either the gloss_qty or poster_qty is over 1000.*/
    SELECT *
        FROM orders
    WHERE standard_qty = 0 AND (gloss_qty > 1000 OR poster_qty> 1000);

    /*Find all the company names that start with a 'C' or 'W', and the primary contact contains 'ana' or 'Ana', but it doesn't contain 'eana'.*/
    SELECT *
        FROM accounts
    WHERE (name LIKE 'C%' OR name LIKE 'W%') 
    AND (primary_poc LIKE '%ana%' OR primary_poc LIKE '%Ana%') 
    AND primary_poc NOT LIKE '%eana%' ;
    ```


    </br>
    </br>
    </br>

# Order of the key words
```SQL
SELECT col1, col2
    FROM table1
  WHERE col3  > 5 AND col4 LIKE '%os%'
  ORDER BY col5
  LIMIT 10;
```

# Commands
You have already learned a lot about writing code in SQL! Let's take a moment to recap all that we have covered before moving on:

| Statement |How to Use It              | Other Details        
| ----------|:--------------------------|:-------------
SELECT	    |SELECT Col1, Col2, ...	    |Provide the columns you want
FROM	    |FROM Table	                |Provide the table where the columns exist
LIMIT	    |LIMIT 10	                |Limits based number of rows returned
ORDER BY	|ORDER BY Col	            |Orders table based on the column. Used with DESC.
WHERE	    |WHERE Col > 5	            |A conditional statement to filter your results
LIKE	    |WHERE Col LIKE '%me%'	    |Only pulls rows where column has 'me' within the text
IN	        |WHERE Col IN ('Y', 'N')	|A filter for only rows with column of 'Y' or 'N'
NOT	        |WHERE Col NOT IN ('Y', 'N')    |NOT is frequently used with LIKE and IN
AND	        |WHERE Col1 > 5 AND Col2 < 3	|Filter rows where two or more conditions must be true
OR	        |WHERE Col1 > 5 OR Col2 < 3	    |Filter rows where at least one condition must be true
BETWEEN	    |WHERE Col BETWEEN 3 AND 5	|Often easier syntax than using an AND



