### Good, General Tips
- Enumeration is an iterative process. 
	- So, once we have the initial Nmap port scans, it's always great to perform deeper analysis of those discovered ports, along with any known open ports as well.
	- Don't forget to document these for later use!
- Follow a similar process that was used in solving `Nibbles`:
	- Enumeration/Scanning with `Nmap` - perform a quick scan for open ports followed by a full port scan
	- Web Footprinting - check any identified web ports for running web applications, and any hidden files/directories. Useful tools for this phase include `whatweb` and `Gobuster`
		- If you identify the website URL, add it to the '/etc/hosts' file with the IP you get in the question below to load it normally to make it easier to track.
		- Note that this is highly recommended, it is optional in solving boxes.
	- After identifying the technologies in use, use tools like `Searchsploit` to find public exploits or search on Google for manual exploitation techniques
	- After gaining an initial foothold, use the `Python3 pty` trick to upgrade to a pseudo TTY
	- Perform manual/automated enumeration of the file system, looking for misconfigurations, services with known vulnerabilities, and sensitive data in cleartext such as credentials
	- Document this data to find ways to escalate privileges to root on this target
- Two ways to get a foothold into a system: using `Metasploit` and a more manual process
	- Always try to work through it by trying both methods!
- We can escalate privileges to root by using helper scripts such as [LinEnum](https://github.com/rebootuser/LinEnum) and [LinPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS).
	- These filter through the system, looking for well-known privilege escalation techniques.
- Have fun, never stop learning, and `think outside of the box`!

### Questions
- Spawn the target, gain a foothold and submit the contents of the user.txt flag.
	- 7002d65b149b0a4d19132a66feed21d8
- After obtaining a foothold on the target, escalate privileges to root and submit the contents of the root.txt flag.
	- f1fba6e9f71efb2630e6e34da6387842