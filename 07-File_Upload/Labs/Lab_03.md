
# File_upload

## Web shell upload via path traversal

### Problem

- This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability.

- To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

- You can log in to your own account using the following credentials: `wiener:peter`.

### Solution 

- Connect to burp and login with given Credintial After Login into wiener upload  the test.php file.

- Then sent the request `myaccount/avatar` to repeter.

- After that change the file path `test.php` to `..%2ftest.php` and send the request.

- Refresh the web page and see the request `files/avatar/..%2ftest.php` in burp change it to `files/avatar/../test.php`

- See the secret key `fMIkVWH3be6zzlgj0mUtKqQbqgn52D0f`.

- Lab solved!!

