Flow control is crucial for writing efficient and error-free scripts. By controlling the flow, we ensure that our script performs the right actions based on the given conditions and user input. The main components of flow control include branches and loops, which allow the script to make decisions and repeat actions as needed.

#### **1. Branches**
- **If-Else Conditions:** Used to execute code based on whether a condition is true or false.
- **Case Statements:** Useful for executing different blocks of code based on the value of a single variable.

#### **2. Loops**
- **For Loops:**
    - Iterates over a list, array, or range, executing commands for each element.
    - Commonly used to process multiple values or execute commands for each item in a list.
    - **Syntax Examples:**
        - `for variable in 1 2 3 4; do echo $variable; done`
        - `for ip in "10.10.10.170 10.10.10.174"; do ping -c 1 $ip; done`
- **While Loops:**
    - Repeats a block of code as long as a specified condition is true.
    - Often uses a counter to avoid infinite loops.
    - Can be combined with if-else conditions for more complex logic.
    - **Syntax Example:**
```
counter=0
while [ $counter -lt 10 ]; do
  ((counter++))
  echo "Counter: $counter"
done
```
**Until Loops:**
- Similar to while loops but runs until a condition becomes true.
- Useful when you want to keep looping until a specific condition is met.
- **Syntax Example:**
```
counter=0
until [ $counter -eq 10 ]; do
  ((counter++))
  echo "Counter: $counter"
done
```
### **Examples from `CIDR.sh` Script**
- **For Loop:** Used to iterate over IP addresses, performing actions like `whois` queries to determine network ranges.
- **While Loop:** Monitors host availability with ping checks, using a counter to ensure the loop stops after a condition is met.
- **Until Loop:** Rarely used but can run until a specific condition becomes false, making it useful for scenarios where you expect a certain state to change.

### **Output Control with `tee`**
- `tee` allows you to view command output in real-time while simultaneously writing it to a file.
- Useful in scripts where you want to monitor progress while saving results for later analysis.
- **Example Usage:**
```
netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
```
### **Exercise Script**
- Demonstrates the use of flow control structures within a script to manage decryption functions and output based on the value of variables.

### Questions
- Create a "For" loop that encodes the variable "var" 28 times in "base64". The number of characters in the 28th hash is the value that must be assigned to the "salt" variable.
	- HTBL00p5r0x