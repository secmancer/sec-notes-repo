## Assembling & Disassembling Notes

### **Overview**
- **Assembling**: The process of converting **Assembly code** into **machine code** using tools like `nasm`.
- **Linking**: Combines the assembled object file with necessary system libraries using `ld`, producing an executable.
- **Disassembling**: The reverse of assembling, converting machine code back into assembly using `objdump` to analyze how the assembler translated the code.

---

### **Assembling the Code**

#### **Steps to Assemble a Basic Assembly File**
1. **Write the Assembly File**:
   - Example file: `helloWorld.s`
   - Use **`.s` or `.asm` extensions** for assembly files.
   - Example code:
     ```nasm
     global _start

     section .data
         message db "Hello HTB Academy!"
         length  equ $-message

     section .text
     _start:
         mov rax, 1
         mov rdi, 1
         mov rsi, message
         mov rdx, length
         syscall

         mov rax, 60
         mov rdi, 0
         syscall
     ```
   - **equ** dynamically calculates the length of `message` instead of using a static value.

2. **Assemble the File** using `nasm`:
   ```bash
   nasm -f elf64 helloWorld.s
   ```
   - `-f elf64`: Specifies **64-bit architecture** for ELF file format.
   - Output: Creates an object file `helloWorld.o` (not yet executable).

---

### **Linking the Object File**
- After assembling, the **object file** needs to be linked to create an executable.
- Use the **`ld`** tool to link the object file and create the final executable.
  
  Command:
  ```bash
  ld -o helloWorld helloWorld.o
  ```
  - Output: Creates an executable `helloWorld`.

3. **Run the Executable**:
   ```bash
   ./helloWorld
   ```
   - Output: `Hello HTB Academy!`

---

### **Automating Assembly and Linking**
- Create a **bash script** to automate the assembly, linking, and execution process:
  ```bash
  #!/bin/bash
  fileName="${1%%.*}"

  nasm -f elf64 ${fileName}.s
  ld ${fileName}.o -o ${fileName}
  [ "$2" == "-g" ] && gdb -q ${fileName} || ./${fileName}
  ```
- To use the script:
  1. Save it as `assembler.sh`.
  2. Make it executable: `chmod +x assembler.sh`.
  3. Run the script: `./assembler.sh helloWorld.s`.

---

### **Disassembling the Code**

#### **Using `objdump` for Disassembly**
- **Disassembling** converts the machine code back to Assembly to see how the assembler translated the instructions.
- Use **`objdump`** to disassemble the ELF executable:
  ```bash
  objdump -M intel -d helloWorld
  ```
  - `-M intel`: Outputs disassembly in **Intel syntax**.
  - `-d`: Disassembles the **`.text` section** (code section).
  
  **Example Output**:
  ```bash
  helloWorld: file format elf64-x86-64

  Disassembly of section .text:

  0000000000401000 <_start>:
    401000:	b8 01 00 00 00       	mov    eax,0x1
    401005:	bf 01 00 00 00       	mov    edi,0x1
    40100a:	48 be 00 20 40 00 00 	movabs rsi,0x402000
    401014:	ba 12 00 00 00       	mov    edx,0x12
    401019:	0f 05                	syscall
    40101b:	b8 3c 00 00 00       	mov    eax,0x3c
    401020:	bf 00 00 00 00       	mov    edi,0x0
    401025:	0f 05                	syscall
  ```

#### **Flags for `objdump`**:
- **Disassemble without showing machine code or addresses**:
  ```bash
  objdump -M intel --no-show-raw-insn --no-addresses -d helloWorld
  ```
  - Output:
    ```bash
    Disassembly of section .text:

    <_start>:
      mov    eax,0x1
      mov    edi,0x1
      movabs rsi,0x402000
      mov    edx,0x12
      syscall 
      mov    eax,0x3c
      mov    edi,0x0
      syscall
    ```

- **Dump only specific sections (e.g., `.data`)**:
  ```bash
  objdump -sj .data helloWorld
  ```
  - Dumps the **`.data` section** where variables are stored.
  
  **Example Output**:
  ```bash
  helloWorld: file format elf64-x86-64

  Contents of section .data:
  402000 48656c6c 6f204854 42204163 6164656d  Hello HTB Academ
  402010 7921                                 y!
  ```

---

### **Summary of Key Steps**
1. **Assembling**: Converts Assembly source code to an **object file**:
   - `nasm -f elf64 helloWorld.s`
2. **Linking**: Creates an **executable** from the object file:
   - `ld -o helloWorld helloWorld.o`
3. **Running**: Execute the file:
   - `./helloWorld`
4. **Disassembling**: Convert the executable back to Assembly to examine the machine code:
   - `objdump -M intel -d helloWorld`

These steps provide a **complete workflow** for writing, assembling, linking, running, and disassembling Assembly code.

## Questions
- Download the attached file and disassemble it to find the flag
	- HBT{d154553m811n9_81n42135_2_f1nd_53c2375}