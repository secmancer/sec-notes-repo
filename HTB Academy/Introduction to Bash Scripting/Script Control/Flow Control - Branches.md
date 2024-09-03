- **Flow Control Branches**:
    - Include `if-else` and `case` statements.
    - `if-else` allows checking any boolean expression.
    - `case` (also known as `switch-case` in languages like C/C++ and C#) only compares a variable to exact values.

- **Case Statements**:
    - **Purpose**: Compares a variable or value against predefined patterns.
    - **Syntax**:
```
case <expression> in
    pattern_1 ) statements ;;
    pattern_2 ) statements ;;
    pattern_3 ) statements ;;
esac
```
- **Components**:
        - **case**: Starts the statement.
        - **expression**: The variable or value to be compared.
        - **pattern_1, pattern_2, ...**: Specific values or patterns to match.
        - **statements**: Code executed if a match is found.
        - **;;**: Ends each pattern's code block.
        - **esac**: Ends the `case` statement.

- **Example in CIDR.sh Script**:
    - **Available Options**:
        1. Identify the network range of the target domain.
        2. Ping discovered hosts.
        3. Perform all checks (both network range identification and pinging hosts).
        4. Exit the script (for any other option).
    - **Script Structure**:
```
case $opt in
    "1") network_range ;;
    "2") ping_host ;;
    "3") network_range && ping_host ;;
    "*") exit 0 ;;
esac
```
**Explanation**:
- The script reads user input (`$opt`) and compares it to predefined options.
- Depending on the input:
    - Executes specific functions (`network_range`, `ping_host`).
    - Executes both functions if option 3 is chosen.
    - Exits the script if any other option is selected.