## CPU Architecture Notes

### **Overview of the CPU**
- **Central Processing Unit (CPU)**: Main processing unit in a computer.
  - **Control Unit (CU)**: Controls and moves data.
  - **Arithmetic/Logic Unit (ALU)**: Performs arithmetic and logical operations.
  
- The efficiency of CPU instruction processing depends on the **Instruction Set Architecture (ISA)**.
  - **RISC (Reduced Instruction Set Computer)**:
    - Uses **simpler instructions**, each requiring multiple cycles.
    - Shorter cycles, requiring **less power** per cycle.
  - **CISC (Complex Instruction Set Computer)**:
    - Uses **more complex instructions**, requiring fewer cycles.
    - Longer cycles, consuming **more power** per instruction.

---

### **Clock Speed & Clock Cycle**
- **Clock speed**: Measures the number of cycles the CPU can execute per second, typically in **Hertz** (Hz).
  - Example: A CPU with **3.0 GHz** clock speed can run **3 billion cycles per second**.
  
- **Clock cycle**: A single tick of the clock, during which a basic operation (e.g., fetching or storing an address) occurs.

- **Multi-core CPUs**: Modern processors can run **multiple clock cycles in parallel** using multiple cores, enhancing performance.

---

### **Instruction Cycle**
- **Instruction Cycle**: The process of executing a single machine instruction.
  - **Stages**:
    1. **Fetch**: Retrieve the next instruction's address from the **Instruction Address Register (IAR)**.
    2. **Decode**: Interpret the fetched instruction from binary format to determine required actions.
    3. **Execute**: Perform the instruction using the **ALU** or **CU** (e.g., arithmetic, logical operations).
    4. **Store**: Write the result to the appropriate destination (register or memory).

- **Example (Assembly Instruction: `add rax, 1`)**:
  1. **Fetch**: Retrieve the binary representation of the instruction (`48 83 C0 01`).
  2. **Decode**: Identify it as an addition operation (`add 1 to rax`).
  3. **Execute**: Retrieve current value of `rax`, add 1.
  4. **Store**: Save the new value to `rax`.

- Modern CPUs can process multiple instructions simultaneously through **parallel processing** with multi-threading and multi-core designs, unlike older CPUs that processed instructions sequentially.

---

### **Processor-Specific Instruction Sets**
- Each processor has its unique **Instruction Set Architecture (ISA)**, meaning the same machine code can represent different instructions across processors.
  - **Example**:
    - Intel x86 machine code `4883C001` = `add rax, 1`
    - ARM machine code `4883C001` = `biceq r8, r0, r8, asr #6`
  
- **ISAs** also differ in syntax representation:
  - Example (x86 architecture):
    - **Intel syntax**: `add rax, 1`
    - **AT&T syntax**: `addb $0x1, %rax`
  
  Both instructions perform the same operation but have different **syntax** and **operand order**.

- The course focuses on the **Intel x86_64 architecture** (also known as **x86_64** or **AMD64**), the most common CPU architecture in modern computers and servers.

---

### **Checking CPU Architecture**
- To check the architecture of a Linux system:
  - **`lscpu` command**: Displays detailed CPU architecture information (e.g., supports **x86_64**, byte order: **Little Endian**).
  - **`uname -m` command**: Displays the CPU architecture.

---

### **Summary**
- **CPU Architecture** determines how a processor processes instructions using its **ISA**.
- **Clock cycles** and **multi-core designs** enable faster, more efficient processing.
- Different processor types (e.g., Intel, ARM) interpret the same machine code differently due to their distinct ISAs.
- Understanding **x86_64 architecture** and its assembly syntax is critical for low-level programming and exploitation on most modern systems.