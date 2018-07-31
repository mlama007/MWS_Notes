# SQL Joins

```SQL
SELECT orders.*,
    accounts.*
    FROM demo.orders
  JOIN demo.accounts
  ON demo.accounts_id = accounts_id;
```


```SQL
-- Pull only account name
SELECT accounts.name, orders.occurred_at
    FROM orders
  JOIN accounts
  ON orders.account_id = accounts.id;

-- pull all the columns from both the accounts and orders table.

SELECT *
    FROM orders
  JOIN accounts
  ON orders.account_id = accounts.id;

-- pull all the information from only the orders table:

SELECT orders.*
    FROM orders
  JOIN accounts
  ON orders.account_id = accounts.id;
```


```SQL
-- Pull all the data from the accounts table, and all the data from the orders table.

SELECT *
	FROM orders
  JOIN accounts
  ON orders.account_id = accounts.id;
 
-- Pull standard_qty, gloss_qty, and poster_qty from the orders table, and the website and the primary_poc from the accounts table.

SELECT orders.standard_qty, 
		orders.gloss_qty,  
        orders.poster_qty,
        accounts.website,
        accounts.primary_poc
	FROM orders
  JOIN accounts
  ON orders.account_id = accounts.id;
```

Order in `ON` doesn't matter

```SQL
SELECT orders.*, accounts.*
    FROM accounts
  JOIN orders
  ON accounts.id = orders.account_id;

-- Notice this result is the same as if you switched the tables in the FROM and JOIN. Additionally, which side of the = a column is listed doesn't matter.

SELECT orders.standard_qty, orders.gloss_qty, 
       orders.poster_qty,  accounts.website, 
       accounts.primary_poc
    FROM orders
  JOIN accounts
  ON orders.account_id = accounts.id
```

</br>

</br>

#  `A primary key exists in every table, and it is a column that has a unique value for every row`

![tables with data](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/59821d7d_screen-shot-2017-08-02-at-11.14.25-am/screen-shot-2017-08-02-at-11.14.25-am.png)

# Keys
`Primary Key (PK)`

A primary key is a unique column in a particular table. This is the first column in each of our tables.

`Foreign Key (FK)`
A foreign key is when we see a primary key in another table.

![table with keys](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/598d2378_screen-shot-2017-08-10-at-8.23.48-pm/screen-shot-2017-08-10-at-8.23.48-pm.png)

</br>

</br>

```SQL
SELECT orders.*
FROM orders
JOIN accounts
ON orders.account_id = accounts.id;
```

Notice our SQL query has the two tables we would like to join - one in the FROM and the other in the JOIN. Then in the ON, we will ALWAYs have the PK equal to the FK:

![table with keys](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/598e0b9e_screen-shot-2017-08-10-at-8.10.13-pm/screen-shot-2017-08-10-at-8.10.13-pm.png)

</br>

# JOIN More than Two Tables
```SQL
SELECT web_events.channel, accounts.name, orders.total
    FROM web_events
  JOIN accounts
  ON web_events.account_id = accounts.id
  JOIN orders
  ON accounts.id = orders.account_id
```

![table with keys](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/598e2e15_screen-shot-2017-08-11-at-3.21.34-pm/screen-shot-2017-08-11-at-3.21.34-pm.png)


# Alias


```SQL
SELECT col1 + col2 AS total, col3
    FROM tablename AS t1
  JOIN tablename2 AS t2
  Before, you saw something like:

-- Produces the exact same results as:

SELECT col1 + col2 total, col3
  FROM tablename t1
  JOIN tablename2 t2
```

## Aliases for Columns in Resulting Table
```SQL
Select t1.column1 aliasname, t2.column2 aliasname2
    FROM tablename AS t1
  JOIN tablename2 AS t2
```

| aliasname |aliasname2   
| ----------|:----------
example row	|example row
example row	|example row

```SQL
/* Provide a table for all web_events associated with account name of Walmart. There should be three columns. Be sure to include the primary_poc, time of the event, and the channel for each event. Additionally, you might choose to add a fourth column to assure only Walmart events were chosen. */

SELECT w.occurred_at,
    w.channel,
    a.primary_poc,
    a.name
	FROM web_events w
  JOIN accounts a
  ON w.account_id = a.id
  WHERE a.name LIKE '%Walmart%';
 
 
/* Provide a table that provides the region for each sales_rep along with their associated accounts. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name. */
SELECT r.name region,
        a.name account,
        s.name rep
  FROM accounts a
  JOIN sales_reps s
  ON a.sales_rep_id = s.id
  JOIN region r
  ON s.region_id = r.id
  ORDER BY a.name;

/*Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. Your final table should have 3 columns: region name, account name, and unit price. A few accounts have 0 for total, so I divided by (total + 0.01) to assure not dividing by zero.
*/
SELECT r.name region,
		a.name account,
        (o.total_amt_usd/(o.total + 0.01)) unit_price
	FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  JOIN sales_reps s
  ON a.sales_rep_id = s.id
  JOIN region r
  ON s.region_id = r.id
```

</br>

</br>

</br>

# JOINs

`JOIN` - an INNER JOIN that only pulls data that exists in both tables.

`LEFT JOIN` - a way to pull all of the rows from the table in the FROM even if they do not exist in the JOIN statement.

`RIGHT JOIN` - a way to pull all of the rows from the table in the JOIN even if they do not exist in the FROM statement.

# Inner Joins
Only returns rows that appear on both tables

![chart of tables](https://i.imgur.com/9uDMtdn.png)

Types of joints that allow to include data that isn't in BOTH tables
![chart of tables](https://i.imgur.com/U0MPn3z.png)
![chart of tables](https://i.imgur.com/Mys65FV.png)

When joining RIGHT (content not shared accross both tables), extra information will be at the bottom
![chart of tables](https://i.imgur.com/s8rfNQc.png)


</br>

</br>

</br>

# JOINs and Filtering

You can filter out certain thing sbefore joining tables:
```SQL
SELECT orders.*
		  accounts.*
	FROM demo.orders
  LEFT JOIN demo.accounts
  ON orders.account_id = accounts.id
  AND accounts.sales_rep_id = 321500
```


```SQL
  /*Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name.*/
  SELECT r.name region,
      s.name sales,
          a.name account
    FROM accounts a
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    WHERE r.name LIKE '%Midwest%'
    ORDER BY a.name;
  
  
  /* Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for accounts where the sales rep has a first name starting with S and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name. */
  SELECT r.name region, 
      s.name rep, 
          a.name account
    FROM accounts a
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    WHERE s.name LIKE 'S%' AND r.name LIKE '%Midwest%'
    ORDER BY a.name;
    
  /* Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for accounts where the sales rep has a last name starting with K and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name.*/

  SELECT r.name region, 
      s.name rep, 
          a.name account
    FROM accounts a
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    WHERE s.name LIKE '% K%' AND r.name LIKE '%Midwest%'
    ORDER BY a.name;
    
  /*Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. However, you should only provide the results if the standard order quantity exceeds 100 and the poster order quantity exceeds 50. Your final table should have 3 columns: region name, account name, and unit price. Sort for the smallest unit price first. In order to avoid a division by zero error, adding .01 to the denominator here is helpful (total_amt_usd/(total+0.01). */
  SELECT r.name region, 
      a.name rep,
          o.total_amt_usd/(o.total+0.01) unit_price
    FROM orders o
    JOIN accounts a
    ON o.account_id = a.id
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    WHERE o.standard_qty > 100 AND o.poster_qty > 50.
    ORDER BY unit_price;
    
  /*Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. However, you should only provide the results if the standard order quantity exceeds 100 and the poster order quantity exceeds 50. Your final table should have 3 columns: region name, account name, and unit price. Sort for the largest unit price first. In order to avoid a division by zero error, adding .01 to the denominator here is helpful (total_amt_usd/(total+0.01). */
  SELECT r.name region, 
      a.name rep,
          o.total_amt_usd/(o.total+0.01) unit_price
    FROM orders o
    JOIN accounts a
    ON o.account_id = a.id
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    WHERE o.standard_qty > 100 AND o.poster_qty > 50.
    ORDER BY unit_price DESC;
    
  /*What are the different channels used by account id 1001? Your final table should have only 2 columns: account name and the different channels. You can try SELECT DISTINCT to narrow down the results to only the unique values.*/
  SELECT DISTINCT a.name,
      w.channel
    FROM web_events w
    JOIN accounts a
    ON w.account_id = a.id
    WHERE a.id = '1001';

  /*Find all the orders that occurred in 2015. Your final table should have 4 columns: occurred_at, account name, order total, and order total_amt_usd.*/
  SELECT DISTINCT a.name,
      o.occurred_at,
          o.total,
          o.total_amt_usd
    FROM accounts a
    JOIN orders o
    ON o.account_id = a.id
    WHERE o.occurred_at BETWEEN '01-01-2015' AND '01-01-2016'
```