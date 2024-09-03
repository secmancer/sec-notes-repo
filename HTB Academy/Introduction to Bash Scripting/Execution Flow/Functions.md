- **Purpose of Functions**:
    - Functions are used to group multiple commands into a single block, improving the clarity and reducing the size of scripts.
    - Functions allow for code reuse, making scripts easier to manage and read.
- **Benefits**:
    - **Clarity**: Functions help organize scripts, making them less chaotic as they grow larger.
    - **Efficiency**: Avoids repetition by enabling the reuse of code for recurring tasks.
- **Defining Functions**:
    - **Method 1**:
```
function name {
    <commands>
}

```
- **Method 2**:
```
name() {
    <commands>
}
```
- Both methods are valid; the choice depends on personal preference. The first method is often preferred for readability due to the explicit use of the keyword "function."
- **Example from CIDR.sh**:
    - **Function Definition**:
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
- **Function Execution**:
```
case $opt in
    "1") network_range ;;
    "2") ping_host ;;
    "3") network_range && ping_host ;;
    "*") exit 0 ;;
esac

```
**Parameter Passing**:
- Functions can accept parameters similar to shell scripts, using `$1`, `$2`, ..., `${n}`, or variables.
- Parameters in functions do not collide with those in other functions or the main script.
- **Example**:
```
function print_pars {
    echo $1 $2 $3
}

one="First parameter"
two="Second parameter"
three="Third parameter"

print_pars "$one" "$two" "$three"

```
- **Global vs. Local Variables**:
    - In Bash, variables defined within a function are global unless declared as `local`.
    - This means they can be accessed and modified outside the function unless explicitly made local.
- **Return Values**:
    - Functions return a status code to the parent process, indicating success or failure.
    - **Common Return Codes**:
        - `0`: Success
        - `1`: General errors
        - `2`: Misuse of shell builtins
        - `126`: Command cannot execute
        - `127`: Command not found
        - `128`: Invalid argument to exit
        - `128+n`: Fatal error signal `n`
        - `130`: Script terminated by Control-C
        - `255*`: Exit status out of range
    - **Capturing Return Codes and Output**:
        - Use `$?` to capture the return code.
        - Use `echo` or assign output to a variable for the function's result.
    - **Example**:
```
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

# Assign result to a variable
content=$(given_args "argument")
echo -e "Content of the variable: \n\t$content"

```
