## GNU Debugger (GDB) Notes

### **Overview**
- **Debugging** is the process of identifying and fixing issues (bugs) in code.
- **GDB** (GNU Debugger) is a powerful tool for debugging **Linux programs**, particularly useful for **Assembly** and **binary exploitation**.
- **Breakpoints** allow us to pause program execution and examine memory and registers to debug efficiently.
  
---

### **Installing GDB and GEF**
- **GDB** is pre-installed in many Linux distributions, including Parrot OS and PwnBox. If not installed, use:
  ```bash
  sudo apt-get update
  sudo apt-get install gdb
  ```

- **GEF (GDB Enhanced Features)** is a plugin for reverse engineering and binary exploitation:
  - Install GEF:
    ```bash
    wget -O ~/.gdbinit-gef.py -q https://gef.blah.cat/py
    echo source ~/.gdbinit-gef.py >> ~/.gdbinit
    ```

---

### **Running GDB with Assembly Code**
1. **Starting GDB**:
   - Run GDB with a binary file:
     ```bash
     gdb -q ./helloWorld
     ```
   - **GEF** will load automatically, shown by the `gef➤` prompt.

2. **Using a Bash Script**:
   - Use the **`assembler.sh` script** (created in earlier sections) to assemble, link, and run GDB in one step:
     ```bash
     ./assembler.sh helloWorld.s -g
     ```

---

### **Basic GDB Commands**

#### **1. General Information**
- **`info` command**: Provides various information about the program.
  - Example: **View functions**:
    ```bash
    gef➤ info functions
    ```
  - Example: **View variables**:
    ```bash
    gef➤ info variables
    ```

#### **2. Help**
- To get help on a specific command, use `help`:
  ```bash
  gef➤ help info
  ```

---

### **Disassembly in GDB**
- To disassemble a function or section, use **`disas`**:
  ```bash
  gef➤ disas _start
  ```
  - Example output:
    ```bash
    Dump of assembler code for function _start:
    0x0000000000401000 <+0>:   mov    eax,0x1
    0x0000000000401005 <+5>:   mov    edi,0x1
    0x000000000040100a <+10>:  movabs rsi,0x402000
    0x0000000000401014 <+20>:  mov    edx,0x12
    0x0000000000401019 <+25>:  syscall
    ```

- **Disassembly** is crucial for understanding the **machine code** and **memory addresses** associated with each instruction.

#### **RIP-Relative Addressing**
- In **Position-Independent Executables (PIE)**, memory addresses are relative to the instruction pointer (`$rip`), instead of absolute addresses, for security reasons.
  - Example: `0x00000000004xxxxx` addresses.
  - Disabling PIE can reduce the risk of **binary exploitation** but is generally used for added security.

---

### **Breakpoints and Examining Data**

#### **Setting Breakpoints**
- **Breakpoints** stop execution at a specified point to examine the program's state.
- Example: Set a breakpoint at the start of a function:
  ```bash
  gef➤ break _start
  ```

#### **Examining Data**
- Once a breakpoint is hit, you can **inspect data** and **variables** in memory:
  - View the contents of a register (e.g., `rax`):
    ```bash
    gef➤ info registers
    ```
  - Examine memory at a specific address:
    ```bash
    gef➤ x/10x $rax
    ```
    - `x/10x` displays **10 hexadecimal values** from the address held in `rax`.

---

### **Useful GDB Commands**
- **Step through instructions**: Use `stepi` (step instruction) to move through code instruction by instruction:
  ```bash
  gef➤ stepi
  ```
- **Continue execution**: Resume execution after hitting a breakpoint:
  ```bash
  gef➤ continue
  ```
- **Print values**: Print the value of a specific variable or register:
  ```bash
  gef➤ print $rax
  ```

---

### **Conclusion**
- **GDB** is a crucial tool for debugging and reverse engineering **Assembly code** and **Linux binaries**.
- Using **breakpoints**, **disassembly**, and **data examination**, GDB allows developers to step through their code, analyze memory, and troubleshoot issues efficiently.