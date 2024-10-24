## Registers, Addresses, and Data Types Notes

### **1. Registers**
- **Registers**: Fastest storage components within the CPU, used to hold data temporarily. They are limited in size and are essential for **assembly programming** and **binary exploitation**.
- Two main types of registers in **x86 architecture**:
  
  #### **Data Registers**
  - Store **instructions** or **syscall arguments**.
  - Primary Data Registers: `rax`, `rbx`, `rcx`, `rdx`
  - Others:
    - **Source Operand**: `rsi`
    - **Destination Operand**: `rdi`
    - **Additional Registers**: `r8`, `r9`, `r10` (used when primary registers are occupied)

  #### **Pointer Registers**
  - Store **address pointers** for specific memory locations.
  - Main Pointer Registers:
    - **Base Stack Pointer (rbp)**: Points to the start of the Stack.
    - **Current Stack Pointer (rsp)**: Points to the current position (top) of the Stack.
    - **Instruction Pointer (rip)**: Holds the address of the next instruction to be executed.

#### **Sub-registers**
- **Registers** are divided into smaller sub-registers for different data sizes.
  - **64-bit** register → `rax`
  - **32-bit** sub-register → `eax`
  - **16-bit** sub-register → `ax`
  - **8-bit** sub-register → `al`
  
- Example: For `rbx` (64-bit), the sub-registers are:
  - **32-bit**: `ebx`
  - **16-bit**: `bx`
  - **8-bit**: `bl`

#### **Key Registers and Sub-registers (x86_64 architecture)**:
| **Description**       | **64-bit** | **32-bit** | **16-bit** | **8-bit** |
|-----------------------|------------|------------|------------|-----------|
| **Syscall Number/Return** | `rax`      | `eax`      | `ax`       | `al`      |
| **Callee Saved**       | `rbx`      | `ebx`      | `bx`       | `bl`      |
| **1st Arg (Dest. Operand)** | `rdi`      | `edi`      | `di`       | `dil`     |
| **2nd Arg (Source Operand)** | `rsi`      | `esi`      | `si`       | `sil`     |
| **3rd Arg**            | `rdx`      | `edx`      | `dx`       | `dl`      |
| **4th Arg (Loop Counter)** | `rcx`      | `ecx`      | `cx`       | `cl`      |
| **5th Arg**            | `r8`       | `r8d`      | `r8w`      | `r8b`     |
| **6th Arg**            | `r9`       | `r9d`      | `r9w`      | `r9b`     |
| **Base Stack Pointer** | `rbp`      | `ebp`      | `bp`       | `bpl`     |
| **Current Stack Pointer** | `rsp`      | `esp`      | `sp`       | `spl`     |
| **Instruction Pointer** | `rip`      | `eip`      | `ip`       | `ipl`     |

---

### **2. Memory Addresses**
- **x86_64 processors** use **64-bit wide addresses** (range: `0x0` to `0xffffffffffffffff`).
- Memory is divided into segments like **Stack**, **Heap**, and **Kernel** regions.
  - Each segment has specific permissions: **Read**, **Write**, or **Execute**.

#### **Addressing Modes** (How the CPU accesses memory):
| **Mode**    | **Description**                         | **Example**        |
|-------------|-----------------------------------------|--------------------|
| **Immediate** | Value is included in the instruction.   | `add 2`            |
| **Register**  | Register holds the value.               | `add rax`          |
| **Direct**    | Full memory address is provided.        | `call 0xffffffffaa8a25ff` |
| **Indirect**  | Pointer to an address is provided.      | `call [rax]`       |
| **Stack**     | Address at the top of the Stack.        | `add rsp`          |

- **Fetching speed**: Immediate > Register > Direct > Indirect > Stack. The further from immediate values, the **slower** the fetch operation.

#### **Understanding Memory Segments**
- Knowledge of address modes is essential for **binary exploitation** (e.g., **Buffer Overflow**, **ROP**, **Heap exploitation**).

---

### **3. Address Endianness**
- **Endianness**: Refers to the **byte order** in which data is stored or retrieved from memory.
  - **Little-Endian**: Least significant byte (smallest) stored **first** (right-to-left).
  - **Big-Endian**: Most significant byte (largest) stored **first** (left-to-right).

#### **Little-Endian Example**:
- Value: `0x0011223344556677`
  - **Little-Endian**: `77 66 55 44 33 22 11 00`
  - **Big-Endian**: `00 11 22 33 44 55 66 77`

#### **Effect on Stored Data**:
- Storing a 2-byte integer (e.g., `426` = `00000001 10101010`):
  - **Little-Endian**: `10101010 00000001` → Changes value to `43521`.
  - **Big-Endian**: Stores it as `00000001 10101010` (no change in value).

- **Important**: Modern **Intel/AMD processors** use **Little-Endian**. Assembly instructions must be written and stored accordingly (right-to-left).

---

### **4. Data Types**
- The **x86 architecture** supports various data sizes used with instructions. 
  - Both **operands** in an instruction must be of the **same size**.

| **Data Type**    | **Length**          | **Example**           |
|------------------|---------------------|-----------------------|
| **Byte**         | 8 bits              | `0xab`                |
| **Word**         | 16 bits (2 bytes)   | `0xabcd`              |
| **Double Word**  | 32 bits (4 bytes)   | `0xabcdef12`          |
| **Quad Word**    | 64 bits (8 bytes)   | `0xabcdef1234567890`  |

#### **Data Type and Register Size**:
| **Sub-register** | **Data Type** |
|------------------|---------------|
| **al**           | **Byte**      |
| **ax**           | **Word**      |
| **eax**          | **Double Word** |
| **rax**          | **Quad Word** |

- **Example**: You cannot use a **byte** variable (`al`) with a **quad word** register (`rax`). Instead, you use the **matching sub-register** (`al` with `al`, `rax` with `rax`).

---

### **Conclusion**
- Understanding **Registers**, **Memory Addresses**, **Endianness**, and **Data Types** is fundamental for writing and debugging **Assembly code**.
- These concepts are also crucial for advanced tasks such as **binary exploitation** and **memory management** in low-level programming.


## Questions
- What is the 8-bit register for 'rdi'?
	- dil