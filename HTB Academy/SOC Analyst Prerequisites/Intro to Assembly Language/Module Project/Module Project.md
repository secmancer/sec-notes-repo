## Module Project Notes: x86 Assembly and Fibonacci Sequence Program

### Overview
- **Objective**: Learn x86 assembly instructions and develop a Fibonacci sequence calculator in assembly.
- **Skills Developed**: Understanding of CPU architecture, assembly language, debugging, and practical application through a calculator program.
- **Context of Use**: Relevant in fields like **penetration testing** and **reverse engineering**; helps interpret low-level operations in a program.

### Key Learning Steps
1. **Data Movement**:
   - Learning **instructions for moving data** and values between **registers** and **memory addresses**.
   
2. **Unary and Binary Instructions**:
   - **Unary Operations**: Instructions with one operand.
   - **Binary Instructions**: Instructions with two operands.
   
3. **Control Instructions and Shellcoding**:
   - Mastery of **control flow instructions** (e.g., loops, conditionals).
   - Introduction to **shellcoding** for advanced control over program execution.

### Fibonacci Sequence Program
- **Goal**: Build a Fibonacci sequence calculator in x86 assembly language as a cumulative project for the module.
  
- **Definition**:
  - A **Fibonacci number** is defined as the sum of the two previous numbers in the sequence:
    \[
    F_n = F_{n-1} + F_{n-2}
    \]
  - **Starting values**: \( F_0 = 0 \) and \( F_1 = 1 \).
  - **Example**: 
    - \( F_2 = F_1 + F_0 = 1 + 0 = 1 \)
    - \( F_3 = F_2 + F_1 = 1 + 1 = 2 \)
    - Continues as: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55...

- **Output for F10**: Sequence would be **0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55**.

### Golden Ratio (Optional Topic)
- **Connection to Fibonacci**: Fibonacci sequence approximates the **Golden Ratio** (Phi, \( \Phi \)), commonly seen in nature and design.
- **Applications**:
  - Widely used in **art**, **architecture**, **design**, and **mathematics**.
  - Featured in **modern branding** and **logo designs**.

### Final Program Functionality
- **Input**: Prompts user for the maximum Fibonacci number to calculate.
- **Output**: Displays all Fibonacci numbers up to the specified maximum.
- **Example Usage**:
  ```
  secmancer@htb[/htb]$ ./fib 

  Please input max Fn
  100
  1
  1
  2
  3
  5
  8
  13
  21
  34
  55
  89
  ```

- **Completion**: By the end of the module, a fully functional Fibonacci sequence calculator will be developed entirely in **x86 assembly**.