## Assembly File Structure Notes

### **Overview**
- An **Assembly file** is structured into different sections to define code, variables, and execution flow.
- Key components: **Labels**, **Instructions**, and **Operands**.
- Assembly files are processed **line-by-line**, with each instruction executed in sequence.

---

### **Basic Structure of an Assembly File**

1. **Global Directive**: 
   - Example: `global _start`
   - Instructs the assembler to **begin execution** at the label `_start`.

2. **Sections**:
   - **`.data` section**: Contains all **variables** to be loaded into memory.
   - **`.text` section**: Contains all **executable code**.
   - These sections correspond to memory segments: the **data segment** and **text segment**.

---

### **Example: Hello World! Assembly Code**
```nasm
global  _start

section .data
message: db      "Hello HTB Academy!"

section .text
_start:
         mov     rax, 1
         mov     rdi, 1
         mov     rsi, message
         mov     rdx, 18
         syscall

         mov     rax, 60
         mov     rdi, 0
         syscall
```
- This code, once assembled and linked, will print `Hello HTB Academy!` to the screen.

---

### **Key Components of an Assembly File**

#### **1. Labels**
- Labels define **locations** in the code that can be referenced by instructions or directives.
- Example: `_start:` is a label that marks where the program begins execution.

#### **2. Instructions and Operands**
- **Instructions** are the operations to be executed (e.g., `mov`, `syscall`).
- **Operands** provide the **values** or **registers** used by the instruction.
- Example:
  - `mov rax, 1`: Move the value `1` into the `rax` register.
  - `mov rsi, message`: Move the address of the `message` label into the `rsi` register.

#### **3. Directives**
- **Directives** give special instructions to the assembler but are not executed at runtime.
- Example: 
  - `global _start`: Directs the program to begin at the `_start` label.
  - **Directives are essential for controlling execution flow and structuring code.**

---

### **Sections of an Assembly File**

#### **1. `.data` Section (Data Segment)**
- **Purpose**: Stores **variables** and **static data** for the program.
- When the program runs, all variables defined here are **loaded into memory** for later use.
- **Defining Variables**:
  - Use **`db`** (define byte), **`dw`** (define word), **`dd`** (define double word), etc.
  - Example:
    ```nasm
    message db "Hello World!", 0x0a  ; Defines a string and newline
    ```

- **Constants**:
  - Use the **`equ`** directive to define constants.
  - Example:
    ```nasm
    message db "Hello World!", 0x0a
    length equ $-message  ; Calculates the length of the string
    ```
  - **`$`** refers to the current address, allowing calculation of the string's length.

#### **2. `.text` Section (Text Segment)**
- **Purpose**: Contains the **executable code** (instructions).
- The **_start** label typically marks where execution begins, as specified by the **global directive**.
- Instructions in this section are loaded into the **text segment** of memory and executed by the CPU.
- **Example**:
  - **System Call**:
    ```nasm
    mov rax, 1       ; Specify system call number (1 = write)
    mov rdi, 1       ; File descriptor (1 = stdout)
    mov rsi, message ; Address of the string (message)
    mov rdx, 18      ; Length of the message (18 bytes)
    syscall          ; Make the system call
    ```

---

### **Memory Protection and Segments**
- The **data segment** (where variables are stored) is **read/write** but **not executable**.
- The **text segment** (where instructions are stored) is **read-only** and **executable**.
- This separation protects against certain binary exploitation techniques (e.g., **buffer overflow**).

---

### **Comments**
- **Comments** start with a semi-colon (`;`) and are used to explain the code for future reference.
- Example:
  ```nasm
  mov rax, 60  ; Exit system call
  ```

---

### **Summary of File Structure**
| **Section**      | **Description**                                                                 |
|------------------|---------------------------------------------------------------------------------|
| `global _start`  | Directive indicating where the program begins execution.                        |
| `.data`          | Contains **variables** to be loaded into memory.                                |
| `.text`          | Contains **executable instructions** to be loaded into the text memory segment.  |

- Understanding the structure of an Assembly file is crucial for writing, assembling, and debugging Assembly programs efficiently.