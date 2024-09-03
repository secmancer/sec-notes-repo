### Arguments in Bash Scripts

- **Special Variables**: These are used to handle command-line arguments.
    
    - `$0`: The name of the script.
    - `$1`, `$2`, ..., `$9`: Up to the 9th argument passed to the script.
    - `$#`: The number of arguments passed to the script.
    - `$@`: All arguments passed to the script.
    - `$?`: The exit status of the last command executed.
    - `$$`: The process ID of the current script.
- **Example Usage**:
```
#!/bin/bash

if [ $# -eq 0 ]; then
  echo -e "You need to specify the target domain.\n"
  echo -e "Usage:"
  echo -e "\t$0 <domain>"
  exit 1
else
  domain=$1
fi

```
- In this example:
    
    - `$#` checks if no arguments were passed.
    - `$0` shows the script name in the usage message.
    - `$1` is used to assign the first argument to the `domain` variable.

### Variables

- **Assignment**:
    
    - Variables are assigned without the dollar sign (`$`), e.g., `variable="value"`.
    - To use the value, prepend the dollar sign, e.g., `echo $variable`.
- **Common Mistake**:
    
    - Incorrect: `variable = "value"` (spaces around `=` cause an error).
    - Correct: `variable="value"` (no spaces around `=`).

### Arrays

- **Declaring Arrays**:
    
    - `domains=(value1 value2 value3 ...)` creates an array with indexed values starting from 0.
- **Accessing Array Elements**:
    
    - Use `${array[index]}` to access an element.
- **Example**:
```
#!/bin/bash

domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)

echo ${domains[0]}  # Outputs: www.inlanefreight.com

```
**Handling Spaces**:

- If values include spaces, quote them to ensure they're treated as single elements, e.g., `domains=("value with spaces" value2)
```
#!/bin/bash

domains=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
echo ${domains[0]}  # Outputs: www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com

```


### Questions:
- Submit the echo statement that would print "www2.inlanefreight.com" when running the last "Arrays.sh" script.
	- echo ${domains[1]}
