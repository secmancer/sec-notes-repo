### Introduction
- Bash is a scripting language used to interact with Unix-based OS and give commands to the system. Since May 2019, Windows supports Bash via the Windows Subsystem for Linux (WSL).
- Unlike programming languages, scripting languages like Bash do not require compilation to execute.
- As penetration testers, proficiency in both Windows and Unix-based systems is essential, especially for tasks like privilege escalation.
- On Unix-based systems, learning how to use the terminal, filter data, and automate tasks is crucial, especially when dealing with large data sets in enterprise networks.
- Scripting increases efficiency by automating tasks and combining commands to process results quickly.
- Like programming languages, Bash scripting has key components: Input & Output, Arguments, Variables & Arrays, Conditional Execution, Arithmetic, Loops, Comparison Operators, and Functions.
- Scripting is often used to automate repetitive tasks or process large amounts of information. Scripts are executed by an interpreter, like Bash, which processes the specified script.



### Script Execution - Examples
```shell-session
secmancer@htb[/htb]$ bash script.sh <optional arguments>
```
```shell-session
secmancer@htb[/htb]$ sh script.sh <optional arguments>
```
```shell-session
secmancer@htb[/htb]$ ./script.sh <optional arguments>
```
- Let us look at such a script and see how they can be created to get specific results. 
- If we execute this script and specify a domain, we see what information this script provides.



### CIDR.sh - Running the script
```shell-session
secmancer@htb[/htb]$ ./CIDR.sh inlanefreight.com

Discovered IP address(es):
165.22.119.202

Additional options available:
	1) Identify the corresponding network range of target domain.
	2) Ping discovered hosts.
	3) All checks.
	*) Exit.

Select your option: 3

NetRange for 165.22.119.202:
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16

Pinging host(s):
165.22.119.202 is up.

1 out of 1 hosts are up.
```
- Now let us look at that script in detail and read it line by line in the best possible way. 
- In the next sections, we will look at and analyze all the parts of this script.



### CIDR.sh - Source Code
```bash
#!/bin/bash

# Check for given arguments
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi

# Identify Network range for the specified IP address(es)
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}

# Ping discovered IP address(es)
function ping_host {
	hosts_up=0
	hosts_total=0
	
	echo -e "\nPinging host(s):"
	for host in $cidr_ips
	do
		stat=1
		while [ $stat -eq 1 ]
		do
			ping -c 2 $host > /dev/null 2>&1
			if [ $? -eq 0 ]
			then
				echo "$host is up."
				((stat--))
				((hosts_up++))
				((hosts_total++))
			else
				echo "$host is down."
				((stat--))
				((hosts_total++))
			fi
		done
	done
	
	echo -e "\n$hosts_up out of $hosts_total hosts are up."
}

# Identify IP address of the specified domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)

echo -e "Discovered IP address:\n$hosts\n"
ipaddr=$(host $domain | grep "has address" | cut -d" " -f4 | tr "\n" " ")

# Available options
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```
- As we can see, we have commented here several parts of the script into which we can split it.
	1. Check for given arguments
	2. Identify network range for the specified IP address(es)
	3. Ping discovered IP address(es)
	4. Identify IP address(es) of the specified domain
	5. Available options



### Script Breakdown
- #### 1. Check for given arguments
	- In the first part of the script, we have an if-else statement that checks if we have specified a domain representing the target company.
- #### 2. Identify network range for the specified IP address(es)
	- Here we have created a function that makes a "whois" query for each IP address and displays the line for the reserved network range, and stores it in the CIDR.txt.
- #### 3. Ping discovered IP address(es)
	- This additional function is used to check if the found hosts are reachable with the respective IP addresses. With the For-Loop, we ping every IP address in the network range and count the results.
- #### 4. Identify IP address(es) of the specified domain
	- As the first step in this script, we identify the IPv4 address of the domain returned to us.
- #### 5. Available Options
	- Then we decide which functions we want to use to find out more information about the infrastructure.