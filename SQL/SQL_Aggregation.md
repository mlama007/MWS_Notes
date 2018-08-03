# SQL Aggregation

Count
Sum
Min 
Max
Average

# Null
Null = No data

```SQL
SELECT col1, col2
    FROM table1
  WHERE primary_poc IS NULL
```

# COUNT

```SQL
  SELECT COUNT(*) AS order_count
      FROM demo.orders o
    WHERE o.occurred_at >= '2015-12-01'
      AND o.occurred_at < '2016-01-01'
  ```

  __Notice that COUNT does not consider rows that have NULL values. Therefore, this can be useful for quickly identifying which rows have missing data.__

  __Unlike COUNT, you can only use SUM on numeric columns. However, SUM will ignore NULL values, as do the other aggregation functions you will see in the upcoming lessons.__

  ```SQL
  /*Find the total amount of poster_qty paper ordered in the orders table.
  */
  SELECT SUM(poster_qty)
    FROM orders;

  /*Find the total amount of standard_qty paper ordered in the orders table.
  */
  SELECT SUM(standard_qty)
    FROM orders;
      
  /*Find the total dollar amount of sales using the total_amt_usd in the orders table.
  */
  SELECT SUM(total_amt_usd)
    FROM orders;
      
  /*Find the total amount spent on standard_amt_usd and gloss_amt_usd paper for each order in the orders table. This should give a dollar amount for each order in the table.*/
  SELECT standard_amt_usd + gloss_amt_usd AS total_spent
    FROM orders;
      
  /*Find the standard_amt_usd per unit of standard_qty paper. Your solution should use both an aggregation and a mathematical operator.*/
  SELECT SUM(standard_amt_usd)/SUM(standard_qty) AS cost_perUnit
    FROM orders;
```
</br>

# MIN & MAX

```SQL
  SELECT MIN(standard_qty) AS standard_min
  SELECT MIN(gloss_qty) AS gloss_min
    FROM orders;
```

</br>

# MIN & MAX

```SQL
  SELECT AVG(standard_qty) AS standard_avg
  SELECT AVG(gloss_qty) AS gloss_avg
    FROM orders;

  /*When was the earliest order ever placed? You only need to return the date.
  */
  SELECT MIN(occurred_at) AS order_date_min
    FROM orders;

  /*Try performing the same query as in question 1 without using an aggregation function. 
  */
  SELECT occurred_at
    FROM orders
    ORDER BY occurred_at
    LIMIT 1;

  /*When did the most recent (latest) web_event occur?
  */
  SELECT MAX(occurred_at) AS lastest_web_event
    FROM web_events;

  /*Try to perform the result of the previous query without using an aggregation function.
  */
  SELECT occurred_at
    FROM web_events
    ORDER BY occurred_at
    LIMIT 1;

  /*Find the mean (AVERAGE) amount spent per order on each paper type, as well as the mean amount of each paper type purchased per order. Your final answer should have 6 values - one for each paper type for the average number of sales, as well as the average amount.
  */
  SELECT AVG(standard_amt_usd) AS standard_avg_usd,
        AVG(gloss_amt_usd) AS gloss_avg_usd,
        AVG(poster_amt_usd) AS poster_avg_usd,
        AVG(standard_qty) AS standard_avg_qty,
        AVG(gloss_qty) AS gloss_avg_qty,
        AVG(poster_qty) AS poster_avg_qty
    FROM orders;
```
</br>

# MEDIAN

```SQL
  /*Via the video, you might be interested in how to calculate the MEDIAN. Though this is more advanced than what we have covered so far try finding - what is the MEDIAN total_usd spent on all orders?
  */
  SELECT *
    FROM (SELECT total_amt_usd
          FROM orders
          ORDER BY total_amt_usd
          LIMIT 3457) AS Table1
    ORDER BY total_amt_usd DESC
    LIMIT 2;
```
Since there are 6912 orders - we want the average of the 3457 and 3456 order amounts when ordered. This is the average of 2483.16 and 2482.55. This gives the median of 2482.855. This obviously isn't an ideal way to compute. If we obtain new orders, we would have to change the limit. SQL didn't even calculate the median for us. The above used a SUBQUERY, but you could use any method to find the two necessary values, and then you just need the average of them.

</br>

# GROUP BY

```SQL
SELECT account_id, 
      SUM(poster_qty) AS poster_qty
      SUM(standard_qty) AS standard_qty
      SUM(gloss_qty) AS gloss_qty
    FROM orders;
  GROUP BY account_id
  ORDER BY account_id

  /*Which account (by name) placed the earliest order? Your solution should have the account name and the date of the order.*/
  SELECT a.name,
      o.occurred_at		
    FROM orders o
    JOIN accounts a
    ON o.account_id = a.id
    ORDER BY o.occurred_at
    LIMIT 1;
      
  /*Find the total sales in usd for each account. You should include two columns - the total sales for each company's orders in usd and the company name.
  */
  SELECT a.name,
      SUM(total_amt_usd) AS total_Sales
    FROM orders o
      JOIN accounts a
    ON o.account_id = a.id
      GROUP BY a.name
      ORDER BY total_Sales DESC;

  /*Via what channel did the most recent (latest) web_event occur, which account was associated with this web_event? Your query should return only three values - the date, channel, and account name.
  */
  SELECT a.name,
      w.channel, 
      w.occurred_at
    FROM web_events w
    JOIN accounts a
    ON w.account_id = a.id
    ORDER BY w.occurred_at DESC
    LIMIT 1;
    
  /*Find the total number of times each type of channel from the web_events was used. Your final table should have two columns - the channel and the number of times the channel was used.
  */
  SELECT channel,
      COUNT(channel)
    FROM web_events 
      GROUP BY channel;

  /*Who was the primary contact associated with the earliest web_event? 
  */
  SELECT a.primary_poc
    FROM accounts a
    JOIN web_events w
    ON w.account_id = a.id
    ORDER BY w.occurred_at
    LIMIT 1;
    
  /*What was the smallest order placed by each account in terms of total usd. Provide only two columns - the account name and the total usd. Order from smallest dollar amounts to largest.
  */
  SELECT a.name,
      MIN(o.total_amt_usd) total_usd
    FROM accounts a
    JOIN orders o
    ON o.account_id = a.id
    GROUP BY a.name
    ORDER BY total_usd;
  
  
  /*Find the number of sales reps in each region. Your final table should have two columns - the region and the number of sales_reps. Order from fewest reps to most reps.*/
  SELECT r.name,
      COUNT(s.name) num_reps	
    FROM sales_reps s
    JOIN region r
    ON s.region_id = r.id
    GROUP BY r.name
    ORDER BY num_reps;
```


```SQL
  /*For each account, determine the average amount of each type of paper they purchased across their orders. Your result should have four columns - one for the account name and one for the average quantity purchased for each of the paper types for each account. 
  */
  SELECT a.name,
      AVG(o.standard_qty) AS standard_avg_qty,
          AVG(o.gloss_qty) AS gloss_avg_qty,
          AVG(o.poster_qty) AS poster_avg_qty        
    FROM accounts a
    JOIN orders o
    ON o.account_id = a.id
    GROUP BY a.name;
    
  /*For each account, determine the average amount spent per order on each paper type. Your result should have four columns - one for the account name and one for the average amount spent on each paper type.
  */
  SELECT a.name,
      AVG(o.standard_amt_usd) AS standard_avg_usd,
          AVG(o.gloss_amt_usd) AS gloss_avg_usd,
          AVG(o.poster_amt_usd) AS poster_avg_usd
    FROM accounts a
    JOIN orders o
    ON o.account_id = a.id
    GROUP BY a.name;

  /*Determine the number of times a particular channel was used in the web_events table for each sales rep. Your final table should have three columns - the name of the sales rep, the channel, and the number of occurrences. Order your table with the highest number of occurrences first.
  */
  SELECT s.name,
      w.channel,
      COUNT(w.channel) channel_used
    FROM web_events w
    JOIN accounts a
    ON w.account_id = a.id
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    GROUP BY s.name, w.channel
    ORDER BY channel_used DESC;
    
  /*Determine the number of times a particular channel was used in the web_events table for each region. Your final table should have three columns - the region name, the channel, and the number of occurrences. Order your table with the highest number of occurrences first.
  */
  SELECT r.name,
      w.channel,
      COUNT(w.channel) channel_used
    FROM web_events w
    JOIN accounts a
    ON w.account_id = a.id
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    JOIN region r
    ON s.region_id = r.id
    GROUP BY r.name, w.channel
    ORDER BY channel_used DESC;
```

</br>

# DISTINCT

DISTINCT is always used in SELECT statements, and it provides the unique rows for all columns written in the SELECT statement. 

```SQL
SELECT DISTINCT account_id,
      channel
    FROM web_events
  ORDER BY account_id

  /*Use DISTINCT to test if there are any accounts associated with more than one region.*/
  SELECT a.name as "account name", 
          a.id as "account id", 
          r.name as "region name"
  FROM accounts a
  JOIN sales_reps s
  ON s.id = a.sales_rep_id
  JOIN region r
  ON r.id = s.region_id;

  SELECT DISTINCT id, name
  FROM accounts;

  /*Have any sales reps worked on more than one account?*/
  SELECT s.id, s.name, COUNT(*) num_accounts
  FROM accounts a
  JOIN sales_reps s
  ON s.id = a.sales_rep_id
  GROUP BY s.id, s.name
  ORDER BY num_accounts;

  SELECT DISTINCT id, name
  FROM sales_reps;
```

</br>

# HAVING

HAVING is the “clean” way to filter a query that has been aggregated, but this is also commonly done using a subquery. Essentially, any time you want to perform a WHERE on an element of your query that was created by an aggregate, you need to use HAVING instead.

```SQL
SELECT account_id,
      SUM(total_amt_usd) AS sum_total_amt_usd
    FROM orders
    GROUP BY 1
    HAVING sum_total_amt_usd >= 250000;

    /*How many of the sales reps have more than 5 accounts that they manage?*/
  SELECT s.name,
      COUNT(a.id) AS account_sum
    FROM accounts a
    JOIN sales_reps s
    ON a.sales_rep_id = s.id
    GROUP BY s.name
    HAVING COUNT(a.id) > 5;
  /*How many accounts have more than 20 orders?*/
  SELECT COUNT(a.id) AS account_sum
    FROM accounts a
    HAVING COUNT(a.id) > 20;
    
  /*Which account has the most orders?*/
  SELECT a.name,
      COUNT(o.id) AS num_orders
    FROM accounts a
    JOIN orders o
    ON o.account_id = a.id
    GROUP BY a.name
    ORDER BY num_orders DESC
    LIMIT 1;
    
  /*How many accounts spent more than 30,000 usd total across all orders?*/
  SELECT a.id, a.name, SUM(o.total_amt_usd) total_spent
  FROM accounts a
  JOIN orders o
  ON a.id = o.account_id
  GROUP BY a.id, a.name
  HAVING SUM(o.total_amt_usd) > 30000
  ORDER BY total_spent DESC; 
    
  /*How many accounts spent less than 1,000 usd total across all orders?*/
  SELECT a.id, a.name, SUM(o.total_amt_usd) total_spent
  FROM accounts a
  JOIN orders o
  ON a.id = o.account_id
  GROUP BY a.id, a.name
  HAVING SUM(o.total_amt_usd) < 1000
  ORDER BY total_spent DESC; 

  /*Which account has spent the most with us?*/
  SELECT a.id, 
      a.name, 
          SUM(o.total_amt_usd) total_spent
    FROM accounts a
    JOIN orders o
    ON a.id = o.account_id
    GROUP BY a.id, a.name
    ORDER BY total_spent DESC
    LIMIT 1;

  /*Which account has spent the least with us?*/
  SELECT a.id, 
      a.name, 
          SUM(o.total_amt_usd) total_spent
    FROM accounts a
    JOIN orders o
    ON a.id = o.account_id
    GROUP BY a.id, a.name
    ORDER BY total_spent
    LIMIT 1;
    
  /*Which accounts used facebook as a channel to contact customers more than 6 times?*/
  SELECT a.id, a.name, w.channel, COUNT(a.id) AS num_uses
    FROM accounts a
    JOIN web_events w
    ON a.id = w.account_id
    GROUP BY a.id, a.name, w.channel
    HAVING COUNT(a.id) > 6 AND w.channel = 'facebook'
  ORDER BY num_uses;

  /*Which account used facebook most as a channel?*/
  SELECT a.id, a.name, w.channel, COUNT(a.id) AS num_uses
    FROM accounts a
    JOIN web_events w
    ON a.id = w.account_id
    GROUP BY a.id, a.name, w.channel
    HAVING COUNT(a.id) > 6 AND w.channel = 'facebook'
  ORDER BY num_uses DESC
  LIMIT 1;

  /*Which channel was most frequently used by most accounts?*/
  SELECT a.id, a.name, w.channel, COUNT(a.id) AS num_uses
    FROM accounts a
    JOIN web_events w
    ON a.id = w.account_id
    GROUP BY a.id, a.name, w.channel
  ORDER BY num_uses DESC
  LIMIT 1;
```


</br>

# DATE

Dates are stored in year, month, day, hour, minute, second, which helps us in truncating.

`DATE_TRUNC` allows you to truncate your date to a particular part of your date-time column. Common trunctions are day, month, and year. Here is a great blog post by Mode Analytics on the power of this function.


`DATE_PART` can be useful for pulling a specific portion of a date, but notice pulling month or day of the week (dow) means that you are no longer keeping the years in order. Rather you are grouping for certain components regardless of which year they belonged in.

```SQL
SELECT DATE_TRUNC('day', occurred_at) AS day
FROM orders
GROUP BY DATE_TRUNC('day', occurred_at)
ORDER BY DATE_TRUNC('day', occurred_at)
```

```SQL
  SELECT standard_qty, COUNT(*)
  FROM orders
  GROUP BY 1 --(this 1 refers to standard_qty since it is the first of the columns included in the select statement)
  ORDER BY 1 --(this 1 refers to standard_qty since it is the first of the columns included in the select statement)


  --Find the sales in terms of total dollars for all orders in each year, ordered from greatest to least. Do you notice any trends in the yearly sales totals?
  SELECT DATE_PART('year', occurred_at) AS ordder_yearly,
    SUM(total_amt_usd) AS total_spent 
  FROM orders
  GROUP BY 1
  ORDER BY 2 DESC;

  --Which month did Parch & Posey have the greatest sales in terms of total dollars? Are all months evenly represented by the dataset?
  SELECT DATE_PART('month', occurred_at) order_monthly, 		SUM(total_amt_usd) total_spent
      FROM orders
    WHERE occurred_at BETWEEN '2014-01-01' AND '2017-01-01'
    GROUP BY 1
    ORDER BY 2 DESC; 

  --Which year did Parch & Posey have the greatest sales in terms of total number of orders? Are all years evenly represented by the dataset?
  SELECT DATE_PART('year', occurred_at) order_yearly,  			COUNT(*) total_sales
      FROM orders
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 1;

  --Which month did Parch & Posey have the greatest sales in terms of total number of orders? Are all months evenly represented by the dataset?
  SELECT DATE_PART('month', occurred_at) order_monthly,
      COUNT(*) total_sales
      FROM orders
    WHERE occurred_at BETWEEN '2014-01-01' AND '2017-01-01'
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 1; 

  --In which month of which year did Walmart spend the most on gloss paper in terms of dollars?
  SELECT DATE_TRUNC('month', o.occurred_at) order_month, 
        SUM(o.gloss_amt_usd) amt_spent
      FROM orders o 
    JOIN accounts a
    ON a.id = o.account_id
    WHERE a.name = 'Walmart'
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 1;
```


</br>

# CASE

```SQL
-- Let's see how we can use the CASE statement to get around this error.
SELECT id, account_id, standard_amt_usd/standard_qty AS unit_price
FROM orders
LIMIT 10;

-- Now, let's use a CASE statement. This way any time the standard_qty is zero, we will return 0, and otherwise we will return the unit_price.
SELECT account_id, CASE WHEN standard_qty = 0 OR standard_qty IS NULL THEN 0
                        ELSE standard_amt_usd/standard_qty END AS unit_price
FROM orders
LIMIT 10;
```

```SQL
--We would like to understand 3 different branches of customers based on the amount associated with their purchases. The top branch includes anyone with a Lifetime Value (total sales of all orders) greater than 200,000 usd. The second branch is between 200,000 and 100,000 usd. The lowest branch is anyone under 100,000 usd. Provide a table that includes the level associated with each account. You should provide the account name, the total sales of all orders for the customer, and the level. Order with the top spending customers listed first.
  SELECT a.name, SUM(total_amt_usd) total_spent, 
      CASE WHEN SUM(total_amt_usd) > 200000 THEN 'top'
      WHEN  SUM(total_amt_usd) > 100000 THEN 'middle'
      ELSE 'low' END AS customer_level
  FROM orders o
  JOIN accounts a
  ON o.account_id = a.id 
  GROUP BY a.name
  ORDER BY 2 DESC;

-- We would now like to perform a similar calculation to the first, but we want to obtain the total amount spent by customers only in 2016 and 2017. Keep the same levels as in the previous question. Order with the top spending customers listed first.
  SELECT a.name, SUM(total_amt_usd) total_spent, 
      CASE WHEN SUM(total_amt_usd) > 200000 THEN 'top'
      WHEN  SUM(total_amt_usd) > 100000 THEN 'middle'
      ELSE 'low' END AS customer_level
  FROM orders o
  JOIN accounts a
  ON o.account_id = a.id
  WHERE occurred_at > '2015-12-31' 
  GROUP BY 1
  ORDER BY 2 DESC;

-- We would like to identify top performing sales reps, which are sales reps associated with more than 200 orders. Create a table with the sales rep name, the total number of orders, and a column with top or not depending on if they have more than 200 orders. Place the top sales people first in your final table.
  SELECT s.name, COUNT(*) num_ords,
      CASE WHEN COUNT(*) > 200 THEN 'top'
      ELSE 'not' END AS sales_rep_level
  FROM orders o
  JOIN accounts a
  ON o.account_id = a.id 
  JOIN sales_reps s
  ON s.id = a.sales_rep_id
  GROUP BY s.name
  ORDER BY 2 DESC;

-- The previous didn't account for the middle, nor the dollar amount associated with the sales. Management decides they want to see these characteristics represented as well. We would like to identify top performing sales reps, which are sales reps associated with more than 200 orders or more than 750000 in total sales. The middle group has any rep with more than 150 orders or 500000 in sales. Create a table with the sales rep name, the total number of orders, total sales across all orders, and a column with top, middle, or low depending on this criteria. Place the top sales people based on dollar amount of sales first in your final table.
  SELECT s.name, COUNT(*), SUM(o.total_amt_usd) total_spent, 
      CASE WHEN COUNT(*) > 200 OR SUM(o.total_amt_usd) > 750000 THEN 'top'
      WHEN COUNT(*) > 150 OR SUM(o.total_amt_usd) > 500000 THEN 'middle'
      ELSE 'low' END AS sales_rep_level
  FROM orders o
  JOIN accounts a
  ON o.account_id = a.id 
  JOIN sales_reps s
  ON s.id = a.sales_rep_id
  GROUP BY s.name
  ORDER BY 3 DESC;
```