**Broken Authentication and Access Control**
- **Broken Authentication**:
    - Allows attackers to bypass authentication functions.
    - Example: Logging in without valid credentials or elevating user privileges.
    - Example Vulnerability: College Management System 1.2 allows login with input `' or 0=0 #` in the email field.
- **Broken Access Control**:
    - Allows unauthorized access to restricted pages or features.
    - Example: A normal user accessing the admin panel.


**Malicious File Upload**
- **Definition**: Exploits file upload features to upload malicious scripts.
- **Issue**: If file validation is not properly implemented, attackers can upload and execute malicious scripts.
- **Example**: WordPress Plugin Responsive Thumbnail Slider 1.0 allows uploading files with double extensions (e.g., `shell.php.jpg`), enabling execution of malicious scripts.



**Command Injection**
- **Definition**: Allows attackers to inject commands into web applications that execute OS commands.
- **Issue**: Poor input sanitization can lead to execution of unintended commands on the server.
- **Example**: WordPress Plugin Plainview Activity Monitor 20161228 allows injecting commands via the `ip` value by appending `| COMMAND...`.



**SQL Injection (SQLi)**
- **Definition**: Occurs when user input is improperly handled in SQL queries, allowing attackers to execute arbitrary SQL commands.
- **Issue**: Can lead to database manipulation or full control over the database server.
- **Example**: College Management System 1.2 suffers from SQL injection, where an injected SQL query always returns true, allowing unauthorized login and data retrieval.


## Questions
- To which of the above categories does public vulnerability 'CVE-2014-6271' belongs to?
	- Command Injection