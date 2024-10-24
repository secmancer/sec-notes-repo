## Assembly Language Notes

### **Overview**
- Most interactions with computers/smartphones occur via **operating systems** and **applications**, developed using **high-level languages** (e.g., C++, Java, Python).
- Physical components like the **processor** cannot understand high-level languages, as they only process **binary data** (1's and 0's).
- **Assembly language** is a **low-level language** that provides instructions the processor can directly execute.
  - Allows developers to write **human-readable machine instructions**.
  - Assembly code is translated into **machine code** (binary) for the processor.

### **Importance of Assembly Language**
- **Assembly** serves as an intermediary between high-level code and machine code, making it easier to write **processor-specific instructions**.
  - Example:
    - Assembly: `add rax, 1`
    - Machine code (hex): `4883C001`
    - Binary code: `01001000 10000011 11000000 00000001`
- **Machine code** is often represented in **hexadecimal (shellcode)** and can be directly loaded into memory as binary instructions.

### **High-Level vs Low-Level Languages**
- **Assembly language** is unique to each **processor architecture** (e.g., Intel x86, ARM).
- **High-level languages** (like C) abstract processor-specific details, enabling **cross-platform development**.
  - High-level code is compiled into **assembly instructions** for the target processor.
  - The assembly is further translated into **machine code**.
- **Interpreted languages** (e.g., Python, PHP, JavaScript) do not compile directly into machine code.
  - Use **pre-built libraries** (often written in compiled high-level languages like C) to execute commands.
  
### **Compilation Process**
- **Compilation** involves multiple stages:
  1. **High-level code** (e.g., Python, C)
  2. Translated into **Assembly code**
  3. Compiled into **machine code** (hexadecimal/shellcode)
  4. Executed as **binary machine code**
  
- Example transformation:
  - Python code: `print("Hello World!")`
  - Translates into equivalent **C code** using `write()` syscall.
  - The **Assembly equivalent** for Linux syscall would be:
    ```nasm
    mov rax, 1
    mov rdi, 1
    mov rsi, message
    mov rdx, 12
    syscall
    ```
  - The **machine code** (hex) for this Assembly:
    ```shellcode
    48 c7 c0 01
    48 c7 c7 01
    48 8b 34 25
    48 c7 c2 0d
    0f 05
    ```
  - The final **binary machine code**:
    ```binary
    01001000 11000111 11000000 00000001
    01001000 11000111 11000111 00000001
    ```

### **Value of Assembly for Pentesters**
- Understanding **Assembly** is critical for **binary exploitation** in **penetration testing**:
  - **Exploiting compiled programs** requires knowledge of how binaries work.
  - Common exploitation techniques:
    - **Buffer overflows**
    - **ROP chains**
    - **Heap exploitation**
- **Disassembling and debugging** binaries involves tracking assembly instructions through CPU components.
- Exploit developers must write **custom shellcode** and manipulate assembly instructions for **binary exploitation**.

### **Processor Architectures**
- Key architectures for modern exploitation:
  - **Intel x86**: Dominates desktop/laptop CPUs.
  - **ARM**: Increasingly common in **smartphones** and **modern laptops** (e.g., M1 MacBook Pro).
- Knowledge of **Intel x86 Assembly** forms the foundation for learning other architectures like **ARM**. 

### **Conclusion**
- Assembly language bridges the gap between **human-readable instructions** and **machine code**.
- It is essential for **binary manipulation**, **processor-specific optimizations**, and **low-level system programming**.

## Questions
- In the above 'Hello World' example, which Assembly instruction will '00001111 00000101' execute?
	- syscall