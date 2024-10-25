## Debugging with GDB Notes

### **Overview**
- Debugging with GDB involves:
  1. **Break**: Set breakpoints to stop execution at specific points.
  2. **Examine**: Inspect the program’s state at breakpoints.
  3. **Step**: Move through the program one instruction at a time to understand its flow.
  4. **Modify**: Change values in registers or memory to observe effects on execution.

### **1. Break (Setting Breakpoints)**
- **Breakpoints** pause program execution to inspect the program state, registers, and memory at specific points.
- Set a **breakpoint** at a function or specific memory address:
  ```bash
  gef➤ break _start
  ```
  - Output: Breakpoint set at the start of the program, e.g., `Breakpoint 1 at 0x401000`.
- **Run the program** after setting breakpoints:
  ```bash
  gef➤ run
  ```

- To set a breakpoint at a **specific address**, use:
  ```bash
  gef➤ break *0x40100a
  ```

- **Continue** to the next breakpoint without restarting the program:
  ```bash
  gef➤ continue
  ```

- **List current breakpoints** using:
  ```bash
  gef➤ info breakpoints
  ```

---

### **2. Examine (Inspecting Registers, Memory, and Code)**
- **Examine memory/registers** using the `x` command:
  ```bash
  gef➤ x/FMT ADDRESS
  ```
  - **FMT** (format) can include:
    - **Count**: Number of items to examine (e.g., `4`).
    - **Format**: Type of data (e.g., `x` for hex, `s` for string, `i` for instructions).
    - **Size**: Memory size (e.g., `b` for byte, `w` for word, `g` for 8 bytes).
  
#### **Examples of Examination**:
1. **Examine next 4 instructions** starting from `$rip` (instruction pointer):
   ```bash
   gef➤ x/4ig $rip
   ```

2. **Examine a string** at a specific memory address (e.g., `0x402000`):
   ```bash
   gef➤ x/s 0x402000
   ```
   - Output: `"Hello HTB Academy!"`

3. **Examine hex data** at an address (e.g., `0x401000`):
   ```bash
   gef➤ x/wx 0x401000
   ```
   - Output: Hex representation of the machine code, e.g., `0x000001b8`.

4. **View register values**:
   ```bash
   gef➤ info registers
   ```

---

### **3. Step (Stepping Through Instructions)**
- **`stepi` (si)**: Step through **one instruction** at a time.
  ```bash
  gef➤ stepi
  ```
  - Moves to the next instruction and shows the current state.

- **Step multiple instructions**:
  ```bash
  gef➤ stepi 3
  ```

- **`step` (s)**: Step through until the next line of code or exit the function.
  ```bash
  gef➤ step
  ```

- **`next` (n)**: Similar to `step`, but skips over function calls.

---

### **4. Modify (Changing Values at Runtime)**
- **Modify values** to see how they affect program behavior without recompiling.
  
#### **Using GEF's `patch` command**:
- **Patch a string** at a memory address:
  ```bash
  gef➤ patch string 0x402000 "Patched!\\x0a"
  ```

- Modify **register values** using `set`:
  ```bash
  gef➤ set $rdx=0x9
  ```

#### **Example (Patching a String and Modifying Registers)**:
1. Set a breakpoint:
   ```bash
   gef➤ break *0x401019
   ```

2. Run the program:
   ```bash
   gef➤ run
   ```

3. **Patch the string** at `0x402000`:
   ```bash
   gef➤ patch string 0x402000 "Patched!\\x0a"
   ```

4. **Modify the register value**:
   ```bash
   gef➤ set $rdx=0x9
   ```

5. **Continue execution**:
   ```bash
   gef➤ continue
   ```
   - Output: The string `Patched!` is printed as the modified program output.

---

### **Summary**
- **Breakpoints** help to stop execution and inspect the state of a program at specific points.
- **Examine** registers, memory, and instructions to understand how the program operates.
- **Step** through instructions or lines of code to follow program execution.
- **Modify** values in registers and memory to test different scenarios without recompiling the code.
- **GDB** is a powerful tool for debugging, reverse engineering, and testing changes in **Assembly code** and binaries, enabling us to understand a program’s behavior at every step.