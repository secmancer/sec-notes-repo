### Walkthrough for HTB Box: Nibbles (Easy, Linux)
- #### **1. Machine Overview**
	- **Name**: Nibbles
	- **Creator**: mrb3n
	- **OS**: Linux
	- **Difficulty**: Easy
	- **Attack Vectors**:
	    - **User**: Web-based enumeration and exploitation.
	    - **Privilege Escalation**: World-writable file / sudoers misconfiguration.
	- **Resources**:
	    - [IppSec Video](https://www.youtube.com/watch?v=s_0GcRGv6Ds)
	    - [Walkthrough by 0xdf](https://0xdf.gitlab.io/2018/06/30/htb-nibbles.html)
- #### **2. Penetration Testing Approaches**
	1. **Black-Box**:
	    - Minimal to no prior knowledge of the target.
	    - Simulates an external attack scenario.
	2. **Grey-Box**:
	    - Some initial information provided (e.g., IP, OS).
	    - Simulates an internal attacker or malicious insider.
	3. **White-Box**:
	    - Complete access, such as admin credentials, source code, or diagrams.
	    - Comprehensive analysis of potential vulnerabilities.
- For **Nibbles**, we use a **grey-box approach** with knowledge of:
	- Target IP.
	- OS (Linux).
	- Web-based attack vector.
- #### **3. Enumeration Process**
- ##### **Step 1: Initial Nmap Scan**
	- **Command**:
    ```bash
    nmap -sV --open -oA nibbles_initial_scan 10.129.42.190
    ```
	- **Findings**:
	    - **Open Ports**:
	        - `22/tcp`: OpenSSH 7.2p2 (Ubuntu Linux).
	        - `80/tcp`: Apache HTTP server.
	    - **Service Info**: Target runs Linux.
- **Files Saved**:
```plaintext
nibbles_initial_scan.gnmap
nibbles_initial_scan.nmap
nibbles_initial_scan.xml
```
- ##### **Step 2: Full TCP Port Scan**
	- **Command**:
    ```bash
    nmap -p- --open -oA nibbles_full_tcp_scan 10.129.42.190
    ```
	- **Purpose**:
	    - Checks all 65,535 TCP ports for additional services.
	    - Found no additional open ports.
- ##### **Step 3: Scripted Nmap Scans**
	1. **Default Script Scan**:
	    - **Command**:
        ```bash
        nmap -sC -p 22,80 -oA nibbles_script_scan 10.129.42.190
        ```
    - **Findings**:
        - SSH host keys retrieved for `22/tcp`.
        - HTTP service on `80/tcp` with no title (basic HTML page).
    - **Output**:
        ```plaintext
        PORT   STATE SERVICE
        22/tcp open  ssh
        80/tcp open  http
        |_http-title: Site doesn't have a title (text/html).
        ```    
2. **HTTP Enumeration Script**:
    - **Command**:
        ```bash
        nmap -sV --script=http-enum -oA nibbles_nmap_http_enum 10.129.42.190
        ```
    - **Findings**:
        - Enumerates common web directories.
        - Did not reveal significant information.
- ##### **Step 4: Banner Grabbing**
	- **SSH**:
	    - **Command**:
        ```bash
        nc -nv 10.129.42.190 22
        ```
    - **Output**:
        ```plaintext
        SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.8
        ```
- **HTTP**:
    - **Command**:
        ```bash
        nc -nv 10.129.42.190 80
        ```
    - **Output**:
        ```plaintext
        (UNKNOWN) [10.129.42.190] 80 (http) open
        ```
        


### **4. Key Takeaways**
- **Active Ports**:
    - `22/tcp`: SSH (OpenSSH 7.2p2).
    - `80/tcp`: HTTP (Apache web server).
- **Enumeration Steps**:
    - Use multiple scans: initial service detection, full port scan, and script-based scans.
    - Leverage tools like `nc` for manual verification.
- **Next Steps**:
    - Investigate the web application on port 80.
    - Perform further enumeration for potential vulnerabilities.



### Questions
- Run an nmap script scan on the target. What is the Apache version running on the server? (answer format: X.X.XX)
	- 2.4.18