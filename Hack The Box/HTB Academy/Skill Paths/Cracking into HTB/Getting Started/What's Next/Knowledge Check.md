### **Knowledge Check: Attacking Your First Box**
- This exercise will test your understanding and skills by applying the techniques learned in this module. 
- Below is a high-level workflow to guide you.
- Tackle the box methodically, take detailed notes, and enjoy the challenge!



### **Step 1: Enumeration/Scanning**
1. **Perform Nmap Scans:**
    - Start with a quick scan to identify open ports:
        ```bash
        nmap -sV --open -oA initial_scan <TARGET_IP>
        ```
    - Follow with a full TCP port scan:
        ```bash
        nmap -p- --open -oA full_scan <TARGET_IP>
        ```
2. **Analyze the Results:**
    - Note services running on open ports (e.g., HTTP, SSH, FTP).
    - Use service-specific scripts with Nmap:  
        ```bash
        nmap -sC -p <PORTS> <TARGET_IP>
        ```        



### **Step 2: Web Footprinting (If Web Ports Found)**
1. **Identify Web Technologies:**
    - Use tools like WhatWeb or Wappalyzer:
        ```bash
        whatweb http://<TARGET_IP>
        ```
2. **Search for Hidden Directories/Files:**
    - Use Gobuster or Dirb:
        ```bash
        gobuster dir -u http://<TARGET_IP> -w /usr/share/seclists/Discovery/Web-Content/common.txt
        ```
3. **Investigate the Application:**
    - Look for CMS (e.g., WordPress, Joomla) or web frameworks.
    - Review source code for comments or hidden clues.
    - Check for login pages or admin panels.
4. **Search for Exploits:**
    - Use Searchsploit or online resources:        
        ```bash
        searchsploit <APPLICATION_NAME> <VERSION>
        ```
        


### **Step 3: Gaining a Foothold**
1. **Manual Exploitation:**
    - Craft or modify an exploit based on your findings.
    - Test payloads on the target (e.g., uploading a reverse shell).
2. **Metasploit Exploitation (If Applicable):**
    
    - Use Metasploit to search for exploits:
        
        ```bash
        msfconsole
        search <APPLICATION_NAME>
        use <EXPLOIT_MODULE>
        set RHOSTS <TARGET_IP>
        set LHOST <YOUR_IP>
        exploit
        ```
        

---

### **Step 4: Post-Exploitation**
1. **Upgrade Shell:**
    - If you obtain a basic shell, upgrade it to a pseudo-TTY:
        ```bash
        python3 -c 'import pty; pty.spawn("/bin/bash")'
        ```
2. **Enumerate the System:**
    - Perform manual checks for sensitive data:
        ```bash
        cat /etc/passwd
        find / -name "*.conf" 2>/dev/null
        ```
    - Use automated tools like LinPEAS or LinEnum:    
        ```bash
        ./linpeas.sh
        ```        



### **Step 5: Privilege Escalation**
1. **Identify Escalation Vectors:**
    - Check for misconfigured **sudo** permissions:
        ```bash
        sudo -l
        ```
    - Look for SUID/SGID binaries:
        ```bash
        find / -perm -4000 2>/dev/null
        ```
2. **Exploit the Vulnerability:**
    - Use GTFOBins to identify ways to exploit misconfigurations.
    - Append reverse shell commands to writable files if they run with elevated privileges.
3. **Automated Assistance:**    
    - Analyze LinPEAS/LinEnum outputs for potential privilege escalation paths.



### **Step 6: Root the Box**
- After escalating privileges, access the root shell.
- Capture the `root.txt` flag.



### **Step 7: Reflect and Document**
1. **Repeat the Attack:**
    - Try alternate foothold or escalation methods to broaden your understanding.
    - Experiment with different tools to achieve the same result.
2. **Take Notes:**
    - Document every step you performed, including commands, outputs, and observations.
3. **Review Key Learnings:**    
    - Identify areas where you got stuck and research further to strengthen your skills.



### **Challenge: Push Yourself**
- Use **both manual and Metasploit methods** to gain a foothold.
- Discover **both privilege escalation paths**.
- Share your findings with a mentor, colleague, or in a forum to validate your methodology.



### Questions
- Spawn the target, gain a foothold and submit the contents of the user.txt flag.
	- 7002d65b149b0a4d19132a66feed21d8
- After obtaining a foothold on the target, escalate privileges to root and submit the contents of the root.txt flag.
	- f1fba6e9f71efb2630e6e34da6387842