- Let's put together everything we learned in this module and attack our first box without a guide.

### Tips
- Remember that enumeration is an iterative process. 
- After performing our `Nmap` port scans, make sure to perform detailed enumeration against all open ports based on what is running on the discovered ports. 
- Follow the same process as we did with `Nibbles`:
	- Enumeration/Scanning with `Nmap` - perform a quick scan for open ports followed by a full port scan
	- Web Footprinting - check any identified web ports for running web applications, and any hidden files/directories. Some useful tools for this phase include `whatweb` and `Gobuster`
	- If you identify the website URL, you can add it to your '/etc/hosts' file with the IP you get in the question below to load it normally, though this is unnecessary.
	- After identifying the technologies in use, use a tool such as `Searchsploit` to find public exploits or search on Google for manual exploitation techniques
	- After gaining an initial foothold, use the `Python3 pty` trick to upgrade to a pseudo TTY
	- Perform manual and automated enumeration of the file system, looking for misconfigurations, services with known vulnerabilities, and sensitive data in cleartext such as credentials
	- Organize this data offline to determine the various ways to escalate privileges to root on this target
- There are two ways to gain a foothold—one using `Metasploit` and one via a manual process. 
- Challenge ourselves to work through and gain an understanding of both methods.
- There are two ways to escalate privileges to root on the target after obtaining a foothold.
- Make use of helper scripts such as [LinEnum](https://github.com/rebootuser/LinEnum) and [LinPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) to assist you. 
- Filter through the information searching for two well-known privilege escalation techniques.
- Have fun, never stop learning, and do not forget to `think outside of the box`!

### Questions
- Spawn the target, gain a foothold and submit the contents of the user.txt flag.
	- 7002d65b149b0a4d19132a66feed21d8
- After obtaining a foothold on the target, escalate privileges to root and submit the contents of the root.txt flag.
	- f1fba6e9f71efb2630e6e34da6387842