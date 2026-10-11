
# File_Upload

- File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size.

## Impact 

- Which aspect of the file the website fails to validate properly, whether that be its size, type, contents, and so on.
+ The file's type isn't validated properly, and the server configuration allows certain types of file (such as .php and .jsp) to be executed as code. 
+ In this case, an attacker could potentially upload a server-side code file that functions as a web shell, effectively granting them full control over the server.

- What restrictions are imposed on the file once it has been successfully uploaded.
+ If the filename isn't validated properly, this could allow an attacker to overwrite critical files simply by uploading a file with the same name. If the server is also vulnerable to directory traversal, this could mean attackers are even able to upload files to unanticipated locations
+ Failing to make sure that the size of the file falls within expected thresholds could also enable a form of denial-of-service (DoS) attack, whereby the attacker fills the available disk space.


## Prevention

- Check the file extension against a whitelist of permitted extensions rather than a blacklist of prohibited ones. It's much easier to guess which extensions you might want to allow than it is to guess which ones an attacker might try to upload.
- Make sure the filename doesn't contain any substrings that may be interpreted as a directory or a traversal sequence (../).
- Rename uploaded files to avoid collisions that may cause existing files to be overwritten.
- Do not upload files to the server's permanent filesystem until they have been fully validated.
- As much as possible, use an established framework for preprocessing file uploads rather than attempting to write your own validation mechanisms.
