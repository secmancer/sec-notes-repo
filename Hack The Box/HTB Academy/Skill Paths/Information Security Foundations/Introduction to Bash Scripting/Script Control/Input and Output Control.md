### Input Control
- After executing commands and sending requests, we often need to manually decide how to proceed based on the results.
- In some cases, we may define several functions in a script for different scenarios and need to determine which function to execute based on a manual check of the results.
- It's possible that certain scans or activities may not be allowed, requiring manual intervention.
- To handle this, we must know how to make a running script wait for our instructions, as demonstrated in the `CIDR.sh` script where a call is added to decide further steps.
```bash
# Available options
<SNIP>
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
- The first `echo` lines serve as a display menu for the options available to us. 
- With the `read` command, the line with "`Select your option:`" is displayed, and the additional option `-p` ensures that our input remains on the same line. 
- Our input is stored in the variable `opt`, which we then use to execute the corresponding functions with the `case` statement, which we will look at later. 
- Depending on the number we enter, the `case` statement determines which functions are executed.



### Output Control
- We’ve learned about output redirection in the `Linux Fundamentals` module, but one issue is that redirected output doesn’t display on the screen—it gets sent to a file instead.
- As scripts become more complex and take longer to run, we may not want to wait passively for results. The `tee` utility helps by allowing us to see the output immediately while also storing it in the specified files.
- In the `CIDR.sh` script, the `tee` utility is used twice in different ways to handle output in this manner.
```bash
<SNIP>

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

<SNIP>

# Identify IP address of the specified domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)

<SNIP>
```
- When using `tee`, we transfer the received output and use the pipe (`|`) to forward it to `tee`. 
- The "`-a` / `--append`" parameter ensures that the specified file is not overwritten but supplemented with the new results. 
- At the same time, it shows us the results and how they will be found in the file.
```shell-session
secmancer@htb[/htb]$ cat discovered_hosts.txt CIDR.txt

165.22.119.202
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16
```
