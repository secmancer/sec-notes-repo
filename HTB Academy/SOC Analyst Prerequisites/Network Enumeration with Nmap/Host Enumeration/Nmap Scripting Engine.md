### Nmap Scripting Engine (NSE)

The **Nmap Scripting Engine (NSE)** allows users to extend Nmap's functionality using **Lua scripts** to interact with specific services. These scripts can perform tasks ranging from **service discovery** to **vulnerability detection**. NSE scripts are categorized into **14 groups**, each designed for different types of analysis.

---

### NSE Script Categories

| **Category**  | **Description**                                                                 |
| ------------- | ------------------------------------------------------------------------------- |
| **auth**      | Determines authentication credentials.                                          |
| **broadcast** | Broadcasts to discover hosts and adds them to scans.                            |
| **brute**     | Attempts brute-force login using credentials.                                   |
| **default**   | Default scripts executed with the `-sC` option.                                 |
| **discovery** | Evaluates available services on the target.                                     |
| **dos**       | Checks for Denial of Service vulnerabilities (rarely used to avoid disruption). |
| **exploit**   | Attempts to exploit known vulnerabilities.                                      |
| **external**  | Uses external services for further processing.                                  |
| **fuzzer**    | Sends unexpected data to services to find vulnerabilities (time-consuming).     |
| **intrusive** | Runs scripts that might negatively affect the target.                           |
| **malware**   | Detects malware infections.                                                     |
| **safe**      | Runs non-intrusive scripts that don't harm the target.                          |
| **version**   | Extends service version detection.                                              |
| **vuln**      | Detects known vulnerabilities.                                                  |

---

### Ways to Use NSE Scripts

1. **Default Scripts**:
   - Executes default scripts (e.g., service discovery, basic vulnerability checks).
   - **Command**: 
     ```bash
     sudo nmap <target> -sC
     ```

2. **Specific Script Category**:
   - Runs all scripts from a specific category.
   - **Command**:
     ```bash
     sudo nmap <target> --script <category>
     ```

3. **Defined Scripts**:
   - Executes specific scripts by name.
   - **Command**:
     ```bash
     sudo nmap <target> --script <script-name>,<script-name>
     ```

---

### NSE Script Example

- **Scanning SMTP Port** with specific scripts:
  ```bash
  sudo nmap 10.129.2.28 -p 25 --script banner,smtp-commands
  ```
  
  **Output**:
  ```
  PORT   STATE SERVICE
  25/tcp open  smtp
  |_banner: 220 inlane ESMTP Postfix (Ubuntu)
  |_smtp-commands: PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, etc.
  ```
  - The **`banner`** script identifies the **Postfix version** and **Ubuntu OS**.
  - The **`smtp-commands`** script lists available **SMTP commands** for interaction.

---

### Aggressive Scan Option

- **Aggressive Scan (`-A`)** performs:
  - Service detection (`-sV`)
  - OS detection (`-O`)
  - Traceroute (`--traceroute`)
  - Runs default NSE scripts (`-sC`)
  
  **Command**:
  ```bash
  sudo nmap 10.129.2.28 -p 80 -A
  ```

  **Output**:
  ```
  PORT   STATE SERVICE VERSION
  80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
  |_http-title: blog.inlanefreight.com
  |_http-server-header: Apache/2.4.29 (Ubuntu)
  |_http-generator: WordPress 5.3.4
  ```
  - Identifies web server details (Apache 2.4.29, WordPress 5.3.4).
  - Estimates the **operating system** (Linux 96%).

---

### Vulnerability Scanning with NSE Scripts

- Use the **vuln category** to scan for **known vulnerabilities**.
  
  **Command**:
  ```bash
  sudo nmap 10.129.2.28 -p 80 -sV --script vuln
  ```

  **Output**:
  ```
  PORT   STATE SERVICE VERSION
  80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
  | http-enum: 
  |   /wp-login.php: Possible admin folder
  |   /: WordPress version: 5.3.4
  |_ vulners: 
  |   cpe:/a:apache:http_server:2.4.29:
  |      CVE-2019-0211 7.2
  |      CVE-2018-1312 6.8
  ```

  - The **http-enum** script identifies various **WordPress versions** and possible **admin folders**.
  - The **vulners** script checks for **CVE vulnerabilities** associated with Apache 2.4.29.

---

### Key NSE Scanning Options Summary

| **Option**                | **Description**                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| `-sC`                     | Runs default scripts.                                                           |
| `--script <category>`      | Executes all scripts from a specified category (e.g., `--script vuln`).          |
| `--script <script-name>`   | Executes specific scripts by name.                                              |
| `-A`                      | Performs aggressive scan (service, OS detection, and default NSE scripts).       |

For more information on NSE scripts and categories, visit the [NSE Documentation](https://nmap.org/nsedoc/index.html).

## Questions
- Use NSE and its scripts to find the flag that one of the services contain and submit it as the answer.
	- HTB{873nniuc71bu6usbs1i96as6dsv26}