#### **1. Initial Observations**
- Accessing the target IP (`http://10.129.42.190`) displays a simple "Hello world!" message.
- A comment in the page source reveals the existence of the `/nibbleblog/` directory:
    ```html
    <!-- /nibbleblog/ directory. Nothing interesting here! -->
    ```



#### **2. Technology Identification**
- **Command**:
    ```bash
    whatweb 10.129.42.190/nibbleblog/
    ```
- **Findings**:
    - Technologies: HTML5, jQuery, PHP.
    - Blogging Engine: **Nibbleblog** (open-source PHP-based blog engine).
    - Redirects from `/nibbleblog` to `/nibbleblog/`.



#### **3. Vulnerability Identification**
- A Google search for **"Nibbleblog exploit"** reveals a known vulnerability:
    - **Nibbleblog 4.0.3 File Upload Vulnerability**.
    - Allows authenticated attackers to upload malicious PHP files.
    - Exploit targets `/admin.php`.



#### **4. Directory Enumeration**
- Using **Gobuster** to uncover additional directories and files:
	- **Command**:
    ```bash
    gobuster dir -u http://10.129.42.190/nibbleblog/ -w /usr/share/seclists/Discovery/Web-Content/common.txt
    ```
	- **Key Findings**:
	    - `/admin/` (redirects to `/admin.php`).
	    - `/content/` (directory listing enabled).
	    - `/README` (contains version details).



#### **5. Confirming Version**
- Accessing `/README` reveals:
    ```plaintext
    Version: v4.0.3
    Codename: Coffee
    Release date: 2014-04-01
    ```
- This matches the vulnerable version of Nibbleblog.



#### **6. Exploring Directories**
- **Directory Listing**:
    - Browsing `/nibbleblog/content/` reveals:
        - `public/`, `private/`, `tmp/`.
- **Interesting File**:
    - `/nibbleblog/content/private/users.xml`:
        ```xml
        <users>
          <user username="admin">
            <id type="integer">0</id>
            <session_fail_count type="integer">2</session_fail_count>
            <session_date type="integer">1608182184</session_date>
          </user>
          <blacklist type="string" ip="10.10.10.1">
            <date type="integer">1512964659</date>
            <fail_count type="integer">1</fail_count>
          </blacklist>
        </users>
        ```
    - Confirms the username: **admin**.



#### **7. Admin Portal Login**
- Access `/nibbleblog/admin.php`:
    - Requires admin credentials.
- Attempts:
    - Common credentials (e.g., admin:admin, admin:password) fail.
    - Brute-forcing blocked due to IP blacklisting.



#### **8. Configuration File**
- **File**: `/nibbleblog/content/private/config.xml`.
- **Contents**:
    - Includes site details like:
        ```xml
        <name type="string">Nibbles</name>
        <notification_email_to type="string">admin@nibbles.com</notification_email_to>
        ```
    - Indicates "Nibbles" as a potential password.



#### **9. Login Success**
- Using credentials:
    - **Username**: admin.
    - **Password**: nibbles.
- Access granted to the admin portal.



### **Key Takeaways**
1. **Enumeration is Key**:
    - Comments, directory listings, and configuration files often reveal sensitive information.
    - Iterative checks and tool usage (e.g., Gobuster, cURL) ensure thorough coverage.
2. **Process Highlights**:
    - Uncovered `/nibbleblog` and its vulnerable version.
    - Identified valid credentials via configuration clues.
    - Demonstrated iterative enumeration techniques to build a foothold.
3. **Next Steps**:
    - Use the **Nibbleblog File Upload Vulnerability** to gain a foothold on the server.
    - Proceed to privilege escalation.
