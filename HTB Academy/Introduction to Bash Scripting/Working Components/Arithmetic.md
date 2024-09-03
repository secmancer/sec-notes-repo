**Operators Overview:**
- **+** : Addition
- **-** : Subtraction
- ***** : Multiplication
- **/** : Division
- **%** : Modulus (remainder of division)
- **`variable++`** : Increase the value of the variable by 1
- **`variable--`** : Decrease the value of the variable by 1
**Example Script**:
```
#!/bin/bash

increase=1
decrease=1

echo "Addition: 10 + 10 = $((10 + 10))"
echo "Subtraction: 10 - 10 = $((10 - 10))"
echo "Multiplication: 10 * 10 = $((10 * 10))"
echo "Division: 10 / 10 = $((10 / 10))"
echo "Modulus: 10 % 4 = $((10 % 4))"

((increase++))
echo "Increase Variable: $increase"

((decrease--))
echo "Decrease Variable: $decrease"
```
**Output**:
```
Addition: 10 + 10 = 20
Subtraction: 10 - 10 = 0
Multiplication: 10 * 10 = 100
Division: 10 / 10 = 1
Modulus: 10 % 4 = 2
Increase Variable: 2
Decrease Variable: 0
```
### Variable Length in Bash
**Function to Calculate Length:**
- **`${#variable}`**: Returns the length of the variable.
**Example Script**:

```
#!/bin/bash

htb="HackTheBox"
echo ${#htb}
```
**Output**:

```
10
```
### Example Usage in a Loop (`CIDR.sh`):
- Increase and decrease operators are used to control loop behavior.
- Example:
```
((stat--))
((hosts_up++))
((hosts_total++))
```