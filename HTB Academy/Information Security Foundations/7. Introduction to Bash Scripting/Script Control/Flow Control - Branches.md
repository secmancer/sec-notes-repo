**Overview**
- **Case Statements**: Also known as switch-case statements in languages like C, C++, and C#.
- **Difference from If-Else**:
    - **If-Else**: Can check any boolean expression, such as comparisons (e.g., greater than, less than).
    - **Case Statements**: Compares a variable or expression to fixed values only.


**Syntax for Case Statements**
```
case <expression> in
    pattern_1 ) statements ;;
    pattern_2 ) statements ;;
    pattern_3 ) statements ;;
esac
```
**Structure**:
- `case <expression> in`: Starts the case statement.
- `pattern_x ) statements ;;`: Each pattern followed by the statements to execute if the pattern matches. Ends with `;;`.
- `esac`: Ends the case statement (reverse of `case`).



**Example in CIDR.sh**
```
<SNIP>
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
<SNIP>
```
**Options**:
- **"1"**: Executes `network_range` function.
- **"2"**: Executes `ping_host` function.
- **"3"**: Executes both `network_range` and `ping_host` functions.
- '*': Exits the script.