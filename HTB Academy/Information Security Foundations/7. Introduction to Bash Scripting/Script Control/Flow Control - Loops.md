#### **1. Control Structures**
- **Purpose**: To manage the execution flow of scripts efficiently and handle different scenarios through branching and looping.
- **Types of Control Structures**:
    - **Branches**: Control the flow based on conditions.
        - If-Else Conditions
        - Case Statements
    - **Loops**: Repeat a block of code multiple times.
        - For Loops
        - While Loops
        - Until Loops



#### **2. For Loops**
- **Purpose**: To execute a block of code for each item in a list or sequence. Useful for iterating over arrays, files, or a set of values.
- **Syntax Examples**:
- Iterating over a sequence of numbers:
```
for variable in 1 2 3 4
do
  echo $variable
done
```
- Iterating over a list of files:
```
for variable in file1 file2 file3
do
  echo $variable
done
```
- Iterating over IP addresses:
```
for ip in "10.10.10.170 10.10.10.174 10.10.10.175"
do
  ping -c 1 $ip
done
```


**Single Line Command**:
```
for ip in 10.10.10.170 10.10.10.174; do ping -c 1 $ip; done
```


**Example from `CIDR.sh`**:
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



#### **3. While Loops**
- **Purpose**: To execute a block of code as long as a specified condition is true. Useful for tasks that need to run until a certain state is reached.
- **Syntax Example**:
```
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
```
- **Using `break` and `continue`**:**
```
counter=0
while [ $counter -lt 10 ]
do
  ((counter++))
  echo "Counter: $counter"
  if [ $counter == 2 ]
  then
    continue
  elif [ $counter == 4 ]
  then
    break
  fi
done
```




#### **4. Until Loops**
- **Purpose**: To execute a block of code as long as a specified condition is false. The loop continues until the condition becomes true.
- **Syntax Example**:
```
counter=0
until [ $counter -eq 10 ]
do
  ((counter++))
  echo "Counter: $counter"
done
```



#### **5. Exercise Script**
- **Purpose**: Demonstrates the use of loops and conditional statements in a script to decrypt a hash.
- **Script Example**:
```
#!/bin/bash

function decrypt {
  MzSaas7k=$(echo $hash | sed 's/988sn1/83unasa/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/4d298d/9999/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/3i8dqos82/873h4d/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/4n9Ls/20X/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/912oijs01/i7gg/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/k32jx0aa/n391s/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/nI72n/YzF1/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/82ns71n/2d49/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/JGcms1a/zIm12/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/MS9/4SIs/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/Ymxj00Ims/Uso18/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/sSi8Lm/Mit/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/9su2n/43n92ka/g')
  Mzns7293sk=$(echo $MzSaas7k | sed 's/ggf3iunds/dn3i8/g')
  MzSaas7k=$(echo $Mzns7293sk | sed 's/uBz/TT0K/g')

  flag=$(echo $MzSaas7k | base64 -d | openssl enc -aes-128-cbc -a -d -salt -pass pass:$salt)
}

# Variables
var="9M"
salt=""
hash="VTJGc2RHVmtYMTl2ZnYyNTdUeERVRnBtQWVGNmFWWVUySG1wTXNmRi9rQT0K"

# Base64 Encoding Example:
#        $ echo "Some Text" | base64

# For-Loop Example
# Check if $salt is empty
if [[ ! -z "$salt" ]]
then
  decrypt
  echo $flag
else
  exit 1
fi
```


## Questions
- Create a "For" loop that encodes the variable "var" 28 times in "base64". The number of characters in the 28th hash is the value that must be assigned to the "salt" variable.
	- HTBL00p5r0x