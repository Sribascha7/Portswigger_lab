# SQL Injection

- Listed under OWASP's A05:2025 - Injection
- it occurs when an attacker is able to manipulate the SQL queries that a web application sends to its database.
- unauthorised access to sensitive data, bypassed authentication, modified or deleted records, full control of database

## SQl Essential For Injection

### Comments 

- Comments in Sql (--),(#),multiline(/* */)
- ex:SELECT * FROM users WHERE username='admin--' AND password='secret';

### Union 

- Combines the results of two or more SELECT statements into a single result set.(note: both SELECT statements must return the same number of columns)
- ex:SELECT name, age FROM students UNION SELECT username, id FROM admins;
 
### Like & Wildcard

- LIKE operator performs pattern matching on strings. The '%' wildcard matches any sequence of characters,'_' matches exactly one character.
- ex:SELECT * FROM users WHERE username LIKE 'adm%';

### Limit

- LIMIT clause limits the number of rows returned.
- ex: SELECT * FROM users LIMIT 1;      -- returns only the first row
  SELECT * FROM users LIMIT 2, 1;    -- skips 2 rows, returns the 3rd

### String Function

- group_concat() aggregates values from multiple rows into a single comma-separated string. Instead of getting results row by row, you get everything at once.
- ex:SELECT group_concat(username, ':', password SEPARATOR '<br>') FROM users; -- Returns:admin:pass123<br>martin:sec<br>Sriba:Scha

- concat() joins individual value together
- ex:CONCAT(username, ':', password) 

### Detecting Sql Injection

- Enter a single quote(')  if the application returns a database error,Try " some use double quotes(") instead of using (')
- Enter ;--:  if the application behaves differently (e.g., returns different content), the comment syntax is being processed.
- Test OR 1=1: if it changes the results, the input is directly in the query's logic.
- Common injection points {URL parameters, form fields (login, search, comment boxes), cookies, and HTTP headers}

