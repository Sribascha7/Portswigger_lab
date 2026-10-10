# Lab-09 SQL Injection

## SQL injection UNION attack, retrieving data from other tables

### Problem

- This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs.

The database contains a different table called users, with columns called `username` and `password`.

To solve the lab, perform a SQL injection UNION attack that retrieves all `usernames` and `passwords`, and use the information to log in as the `administrator` user.

### Solution 

- GOto => product category filter and  determine number of column it returned by using 'order by':`'ORDER by 2--+`

- So it given that there is `username` and `password` column and a table name:`users` is there so we directly enumurate the username and password using 'union select'`'UNION SELECT username,password from users` .

- Then login as `administrator`

- Lab Solved!!
