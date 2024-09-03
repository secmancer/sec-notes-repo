In Bash scripting, input control allows us to pause a running script and wait for user instructions before proceeding. This is useful when manual decisions are required based on the results of previous commands or when certain actions might not be allowed without user consent.

#### Example: `CIDR.sh`
**Menu for User Input:**

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
- **`echo` commands:** Display a menu of options.
- **`read -p` command:** Prompts the user for input, storing it in the `opt` variable.
- **`case` statement:** Executes the corresponding function based on the user’s input.

### Output Control with `tee`

When a script produces output, it may be redirected to a file for logging purposes. However, redirection typically prevents the output from being displayed on the terminal. To avoid this, the `tee` utility is used to both display the output and save it to a file simultaneously.

**Example Usage in `CIDR.sh`:**

```
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

# Identify IP address of the specified domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)
```
- **`tee -a filename`**: Appends the command's output to the specified file while displaying it in the terminal.
- **Piping with `|`:** Sends the output of a command to `tee`, ensuring that it is captured both in the terminal and the file.