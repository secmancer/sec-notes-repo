#### **Overview of Bash Scripting**
- **Purpose**: Bash is used to communicate with Unix-based OS, executing commands and automating tasks.
- **Windows Compatibility**: Since May 2019, Windows supports Bash via Windows Subsystem for Linux (WSL).
- **Difference from Programming Languages**: Unlike programming languages, scripting languages like Bash do not require compilation; scripts are interpreted and executed directly.

#### **Importance for Penetration Testers**
- **System Proficiency**: Essential to work efficiently across various operating systems, including Unix-based systems.
- **Data Handling**: Ability to handle large datasets, sort, and filter information is crucial in enterprise environments.
- **Automation**: Scripting improves efficiency by automating repetitive tasks and processing data.

#### **Key Elements of Scripting Languages**
- **Input & Output**: Handling user input and displaying results.
- **Arguments, Variables & Arrays**: Storing and managing data.
- **Conditional Execution**: Performing actions based on conditions.
- **Arithmetic**: Performing calculations.
- **Loops**: Repeating tasks.
- **Comparison Operators**: Comparing values.
- **Functions**: Grouping commands into reusable blocks.

#### **Script Execution Examples**
- **Executing a Script**: To run a Bash script, you can use the following commands:
    - `bash script.sh <optional arguments>`
    - `sh script.sh <optional arguments>`
    - `./script.sh <optional arguments>`

#### **Script Example: `CIDR.sh`**
- **Purpose**: The script identifies IP addresses of a domain, determines their network ranges, and pings them to check their availability.
- **Execution**:
    - Command: `./CIDR.sh inlanefreight.com`
    - Example Output:
```
Discovered IP address(es):
165.22.119.202

Additional options available:
    1) Identify the corresponding network range of target domain.
    2) Ping discovered hosts.
    3) All checks.
    *) Exit.

Select your option: 3
```


#### **Script Breakdown**
1. **Check for Given Arguments**
    - **Code**:
```
if [ $# -eq 0 ]
then
    echo -e "You need to specify the target domain.\n"
    echo -e "Usage:"
    echo -e "\t$0 <domain>"
    exit 1
else
    domain=$1
fi
```
2. **Identify Network Range**
	- **Function**: Queries whois for each IP to find and display network ranges and stores results in `CIDR.txt`.
	- **Code**:
```
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
```
3. **Ping Discovered IP Addresses**
	- **Function**: Pings each IP address in the network range to check if it is reachable, counts the results.
	- **Code**:
```
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
```
4. **Identify IP Address(es)**
	- **Code**:
```
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)
echo -e "Discovered IP address:\n$hosts\n"
ipaddr=$(host $domain | grep "has address" | cut -d" " -f4 | tr "\n" " ")
```
5. **Available Options**
	- **Code**:
```
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


#### **Key Takeaways**
- **Script Creation**: Learn to create scripts that handle tasks efficiently, automate processes, and manage large datasets.
- **Bash Proficiency**: Essential for effective work with Unix-based systems and Windows Subsystem for Linux.
- **Continuous Learning**: Mastering scripting languages enhances your ability to handle diverse tasks and improve operational efficiency.