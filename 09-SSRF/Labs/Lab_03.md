
# SSRF

## Blind SSRF with out-of-band detection

### Problem

- This site uses analytics software which fetches the URL specified in the Referer header when a product page is loaded.

- To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator server.

### Solution

- Connect to burp And Open Any product see the request `/product?productId=1` sent it to repeter.

- Open the Burp Collaborator(Pro version),Copy a payload and add in referrer header in repeter.

- Like
```
Referer: https://0a0f00180315d6c883711aa700b50073.web-security-academy.net/
Referer: https://1oqiygw4r4li52godyeat1878yep2fq4.oastify.com
```
- Open the Collaborator and click poll now 

- Lab Solved!!!


