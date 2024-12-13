### Introduction
- A well-organized working environment streamlines penetration testing, saving significant time by reducing the need to repeatedly locate familiar resources. Proper preparation, including gathering and installing necessary tools, can save hours during assessments.
- Corporate networks often consist of diverse operating systems, making it logical to organize hosts and servers by their OS. Structuring the environment according to penetration testing stages and target OS ensures efficiency and clarity in assessments.
```shell-session
secmancer@htb[/htb]$ tree .

.
└── Penetration-Testing
	│
	├── Pre-Engagement
	│       └── ...
    ├── Linux
    │   ├── Information-Gathering
    │   │   └── ...
    │   ├── Vulnerability-Assessment
    │   │   └── ...
    │   ├── Exploitation
    │   │   └── ...
    │   ├── Post-Exploitation
    │   │   └── ...
    │   └── Lateral-Movement
    │       └── ...
    ├── Windows
    │   ├── Information-Gathering
    │   │   └── ...
    │   ├── Vulnerability-Assessment
    │   │   └── ...
    │   ├── Exploitation
    │   │   └── ...
    │   ├── Post-Exploitation
    │   │   └── ...
    │   └── Lateral-Movement
    │       └── ...
    ├── Reporting
    │   └── ...
	└── Results
	    └── ...
```
- Penetration testers should tailor their structure based on their specialization and work style, ensuring it aligns with their strengths and preferences.
- In team settings, it is essential to develop a shared structure that all members understand and can navigate effectively.
- Use examples as a foundation to create a system suited to individual or team needs.
- An example of a layout someone may use is shown below.
```shell-session
secmancer@htb[/htb]$ tree .

.
└── Penetration-Testing
	│
	├── Pre-Engagement
	│       └── ...
    ├── Network-Pentesting
	│       ├── Linux
	│       │   ├── Information-Gathering
	│		│   │   └── ...
	│       │   ├── Vulnerability-Assessment
    │       │   │	└── ...
    │       │	└── ...
    │       │    	└── ...
    │		├── Windows
    │ 		│   ├── Information-Gathering
    │		│   │   └── ...
    │		│   └── ...
    │       └── ...
    ├── WebApp-Pentesting
	│       └── ...
    ├── Social-Engineering
	│       └── ...
    ├── .......
	│       └── ...
    ├── Reporting
    │   └── ...
	└── Results
	    └── ...
```
- Proper organization helps track progress, identify errors, and ensure no critical steps are missed during penetration testing. Saving notes, cheat sheets, and scripts can enhance understanding and streamline future engagements.
- Newcomers should begin with simple structures, such as organizing by operating system, to build a foundation for effective management in penetration testing.
- In team settings, establish clear procedures and roles to ensure consistent workflows, prevent misplacement of files, and safeguard critical evidence for reporting.


### Bookmarks
- Browser add-ons can improve penetration testing activities, and Firefox's account-based synchronization allows seamless transfer of add-ons and bookmarks between environments.
- Avoid storing sensitive or private resources in synchronized accounts to prevent unauthorized access. 
- Customer-related bookmarks should never be saved online, adhering to the principle that stored lists could be viewed by third parties.
- For example, we can use a separate Firefox account for penetration testing. Maintain and edit bookmark lists locally before importing them to the pentesting account for added security.


### Password Manager
- Password managers are valuable tools for both personal use and penetration tests, aiding in managing and utilizing credentials efficiently.
- Password reuse is a common vulnerability in networks, allowing testers to use found or decrypted credentials across multiple systems or services to expand access and attack opportunities.
- There are only three problems with passwords:
	1. Complexity
	2. Re-usage
	3. Remembering
- #### 1. Complexity
	- Creating and remembering complex passwords is challenging for most users, often leading to weak, predictable choices based on familiar content.
	- Frequently used passwords, as highlighted by NordPass’s [most common passwords list](https://nordpass.com/most-common-passwords-list/), can often be guessed within seconds without advanced techniques like password mutation.
- #### 2. Re-usage
	- Even if a user memorizes a strong password, the issue of password reuse remains. Using the same password across multiple services enables attackers to compromise multiple components of an infrastructure.
	- To mitigate this risk, users must create and remember unique, complex passwords for every service, which poses a significant challenge for standard users.
- #### 3. Remembering
	- Password managers address several common password-related issues, benefiting both standard users and penetration testers who work with numerous services and servers requiring strong, unique passwords.
	- Tools like 1Password, LastPass, Keeper, and Bitwarden provide secure storage and easy access to passwords. They allow users to remember only one master password, with some offering additional storage and 2FA options for teams.
	- **Internal Penetration Testing with 1Password**:
	    1. Before testing, regenerate these and enable 2FA.
	    2.  Install the 1Password add-on on the internal host, log in using generated keys, ensuring the 2FA prevents third-party access even if compromised by keyloggers.
	    3. Once logged in, use 1Password to access Firefox accounts, add-ons, and bookmarks effortlessly.


### Updates & Automation
- Continuously update the components (e.g., operating systems, GitHub collections) used for penetration testing. Record all resources and their sources to facilitate future automation and streamline setup.
- Save automation scripts in 1Password for quick access when needed. Scripts are OS-dependent (Bash, Python, PowerShell) and help in system reinstallation and efficient testing.
- Maintain a record of tools, explanations, cheat sheets, and new methods to keep entries up-to-date, ensuring continuous learning and efficiency in penetration testing.


### Note Taking
- Note-taking is another essential part of our penetration testing.
- This is because we accumulate a lot of different information, results, and ideas that are difficult to remember all at once. 
- There are five different main types of information that need to be noted down:
	1. Newly discovered information
	2. Ideas for further tests and processing
	3. Scan results
	4. Logging
	5. Screenshots
- #### 1. Discovered Information
	- This can be information like new IP addresses, usernames, passwords, and source code that are related to the penetration testing engagement/process.
	- Information like this can be obtained multiple ways
		- OSINT
		- Active Scans
		- Manual analysis
	- This can be used against our target company.
- #### 2. Processing
	- With all of this coming in, now we need a way to organize it.
	- Noting down this information will work great, but using note taking apps will allow better organization with our notes, while also making sure we can easily search and find information within our notes.
	- We have a bunch of options for us, but some popular ones are:
		 - [Notion.so](https://notion.so) is a fancy online markdown editor that offers many different functions and gives us the ability to shape our ideas and thoughts according to our preferences.
		- [Xmind](https://www.xmind.net) is an excellent mind map editor that can visualize relevant information components and processes very well.
		- [Obsidian](https://obsidian.md/) is a powerful knowledge base that works on top of a local folder of plain text Markdown files.
- #### 3. Results
	- The results from scans and penetration testing can be overwhelming, especially initially. Experience and practice are key to filtering out critical information effectively.
	- We should keep all information and results to avoid missing important details, as they may be useful later in the engagement. These results are often essential for documentation purposes.
	- Use tools like [GhostWriter](https://github.com/GhostManager/Ghostwriter) or [Pwndoc](https://github.com/pwndoc/pwndoc) to generate structured documentation and maintain a clear record of steps taken during penetration tests.
- #### 4. Logging
	- Logging is crucial for documentation and proving that any damage during a penetration test was not caused by our actions.
	- **Command Line Logging Tools**:
	    - **`date`**: Displays the exact date and time for each command executed in the terminal.
	    - **`script`**: Captures and saves all commands and their results to a background file.
	- Replace the `PS1` variable in `.bashrc` to display date and time alongside prompts for better visibility.
- #### PS1
```bash
PS1="\[\033[1;32m\]\342\224\200\$([[ \$(/opt/vpnbash.sh) == *\"10.\"* ]] && echo \"[\[\033[1;34m\]\$(/opt/vpnserver.sh)\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\$(/opt/vpnbash.sh)\[\033[1;32m\]]\342\224\200\")[\[\033[1;37m\]\u\[\033[01;32m\]@\[\033[01;34m\]\h\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\w\[\033[1;32m\]]\n\[\033[1;32m\]\342\224\224\342\224\200\342\224\200\342\225\274 [\[\e[01;33m\]$(date +%D-%r)\[\e[01;32m\]]\\$ \[\e[0m\]"
```
- #### Date
```shell-session
─[eu-academy-1]─[10.10.14.2]─[Cry0l1t3@htb]─[~]
└──╼ [03/21/21-01:45:04 PM]$
```
- **Logging Tools**:
    - **`script`** (Linux): Captures all commands and results, saving them to a background file.
    - **Start-Transcript** (Windows): Logs all commands and output, allowing for detailed documentation.
- **Naming Convention**: It’s recommended to define a consistent format for saved logs, such as `<date>-<start time>-<name>.log`.
- #### Script
```shell-session
secmancer@htb[/htb]$ script 03-21-2021-0200pm-exploitation.log

secmancer@htb[/htb]$ ...SNIP...
secmancer@htb[/htb]$ exit
```
- #### Start-Transcript
```powershell-session
C:\> Start-Transcript -Path "C:\Pentesting\03-21-2021-0200pm-exploitation.log"

Transcript started, output file is C:\Pentesting\03-21-2021-0200pm-exploitation.log

C:\> ...SNIP...
C:\> Stop-Transcript
```
- Logs will be automatically sorted by timestamp, reducing the need to manually examine them. 
- This improves clarity for team members, making it easier to understand the steps taken and the timing.
- Logging helps analyze approaches to identify repetitive or commonly used steps. Using scripts to automate these steps can save time and improve efficiency.
- Always use tools that allow saving results in separate files, as they may change over time. 
- This enables comparison between current and previous results for a more thorough analysis.
- Tools like [Tmux](https://github.com/tmux/tmux/wiki) and [Terminator](https://terminator-gtk3.readthedocs.io/en/latest/) offer built-in logging features. 
- For tools that don’t support logging, use redirections with `tee` to capture output to files.
    ```bash
    command | tee -a log-file.log  
    ```
- #### Linux Output Redirection
```shell-session
secmancer@htb[/htb]$ ./custom-tool.py 10.129.28.119 > logs.custom-tool
```
```shell-session
secmancer@htb[/htb]$ ./custom-tool.py 10.129.28.119 | tee -a logs.custom-tool
```
- #### Windows Output Redirection
```powershell-session
C:\> .\custom-tool.ps1 10.129.28.119 > logs.custom-tool
```
```powershell-session
C:\> .\custom-tool.ps1 10.129.28.119 | Out-File -Append logs.custom-tool
```
- #### 5. Screenshots
	- Screenshots provide proof of results and serve as a record for Proof-of-Concept and documentation.
	- Flameshot ([GitHub](https://github.com/flameshot-org/flameshot)) is highly recommended for capturing and editing screenshots, eliminating the need for external editing programs.
	- Can be installed via APT package manager or downloaded directly from GitHub.
	- Sometimes, however, we cannot show all the necessary steps in one or more screenshots. We can use an application called [Peek](https://github.com/phw/peek) and create GIFs that record all the required actions for us.