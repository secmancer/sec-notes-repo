#### **1. Input Control**
- **Purpose**: To manage user input and decide how to proceed based on it. This is useful for selecting options and controlling the flow of the script based on user choices or results from previous commands.
- **Example** (from `CIDR.sh`):
```
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
**Explanation**:
- **`echo`**: Displays the menu options.
- **`read -p "Select your option: " opt`**: Prompts the user for input and stores the result in the `opt` variable.
- **`case $opt in ... esac`**: Executes different functions based on the user’s input. The `case` statement helps in branching based on the user's choice.


#### **2. Output Control**
- **Purpose**: To manage the output of commands in scripts, especially when dealing with long-running scripts. This involves displaying output immediately while also saving it to files for later review.
- **Example** (from `CIDR.sh`):
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
**Explanation**:
- **`tee`**: Used to both display the output on the terminal and append it to a file.
    - **`tee -a CIDR.txt`**: Appends the output to `CIDR.txt` and also displays it on the screen.
    - **`tee discovered_hosts.txt`**: Writes the output to `discovered_hosts.txt` and displays it.
- **Pipe (`|`)**: Directs the output of a command into `tee`.



#### **3. Combining Input and Output Control**
- Using **`read`** for input control and **`tee`** for output control ensures that scripts can interact with users and handle their input effectively while also managing and logging output efficiently.