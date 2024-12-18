### Introduction
- As scripts grow larger, they can become chaotic. Using functions helps improve both the size and clarity of the script.
- Functions combine multiple commands into a block between curly brackets (`{` ... `}`) and are called by a user-defined name.
- Functions are essential for executing recurring commands, avoiding repetition, and making code more concise and readable.
- Functions should always be defined logically before their first use, typically at the beginning of the script.
- There are two ways to create functions in Bash.



### Functions
- #### Method 1
```bash
function name {
	<commands>
}
```
- #### Method 2
```bash
name() {
	<commands>
}
```
- We can choose the method to define a function that is most comfortable for us.
- In our `CIDR.sh` script, we used the first method because it is easier to read with the keyword "`function`."



### CIDR.sh
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
```
- The function is called only by calling the specified name of the function, as we have seen in the case statement.



### Function Execution - CIDR.sh
```bash
<SNIP>
case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```




### Parameter Passing
- Such functions should be designed so that they can be used with a fixed structure of the values or at least only with a fixed format. 
- Like we have already seen in our `CIDR.sh` script, we used the format of an IP address for the function "`network_range`". 
- The parameters are optional, and therefore we can call the function without parameters. 
- In principle, the same applies to the passed parameters as to parameters passed to a shell script. 
- These are `$1` - `$9` (`${n}`), or `$variable` as we have already seen.
- Each function has its own set of parameters. 
- So they do not collide with those of other functions or the parameters of the shell script.
- An important difference between bash scripts and other programming languages is that all defined variables are always processed `globally` unless otherwise declared by "[local](https://www.tldp.org/LDP/abs/html/localvar.html)." 
- This means that the first time we have defined a variable in a function, we will call it in our main script (outside the function). 
- Passing the parameters to the functions is done the same way as we passed the arguments to our script.



### PrintPars.sh
```bash
#!/bin/bash

function print_pars {
	echo $1 $2 $3
}

one="First parameter"
two="Second parameter"
three="Third parameter"

print_pars "$one" "$two" "$three"
```
```shell-session
secmancer@htb[/htb]$ ./PrintPars.sh

First parameter Second parameter Third parameter
```



### Return Values
- When we start a new process, each `child process` (for example, a `function` in the executed script) returns a `return code` to the `parent process` (`bash shell` through which we executed the script) at its termination, informing it of the status of the execution. 
- This information is used to determine whether the process ran successfully or whether specific errors occurred. 
- Based on this information, the `parent process` can decide on further program flow.
![[Screenshot_20241111_153521.png]]
- To get the value of a function back, we can use several methods like `return`, `echo`, or a `variable`. 
- In the next example, we will see how to use "`$?`" to read the "`return code`," how to pass the arguments to the function and how to assign the result to a variable.



### Return.sh
```bash
#!/bin/bash

function given_args {

        if [ $# -lt 1 ]
        then
                echo -e "Number of arguments: $#"
                return 1
        else
                echo -e "Number of arguments: $#"
                return 0
        fi
}

# No arguments given
given_args
echo -e "Function status code: $?\n"

# One argument given
given_args "argument"
echo -e "Function status code: $?\n"

# Pass the results of the funtion into a variable
content=$(given_args "argument")

echo -e "Content of the variable: \n\t$content"
```



### Return.sh - Execution
```shell-session
secmancer@htb[/htb]$ ./Return.sh

Number of arguments: 0
Function status code: 1

Number of arguments: 1
Function status code: 0

Content of the variable:
    Number of arguments: 1
```