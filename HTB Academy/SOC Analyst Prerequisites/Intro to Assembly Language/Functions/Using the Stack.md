## Notes on Using the Stack in Assembly

### Overview of the Stack
- **Stack**: A segment of memory used to temporarily store data during program execution.
- **Key Stack Registers**:
  - **`rsp` (Stack Pointer)**: Points to the **top of the stack**.
  - **`rbp` (Base Pointer)**: Often used to refer to the **bottom of the stack**.
- **LIFO (Last-In-First-Out)**: Stack operates on a LIFO basis—**last value pushed** is the **first one popped**.

### Basic Stack Operations
- **`push`**: Copies a register's value to the **top of the stack** and decreases `rsp`.
  - Example: `push rax` (places the value in `rax` at the top of the stack)
- **`pop`**: Moves the **top value of the stack** into a register and increases `rsp`.
  - Example: `pop rax` (retrieves the top stack value into `rax` and removes it from the stack)

| **Instruction** | **Description**                                   | **Example**       |
|-----------------|---------------------------------------------------|-------------------|
| `push`          | Copies value to the top of the stack              | `push rax`       |
| `pop`           | Moves top stack value to a register, removing it  | `pop rax`        |

### How the Stack Works (Example)
1. **Push Sequence**:
   - `push rax` places the value of `rax` at the top.
   - `push rbx` places `rbx` on top of `rax`.
2. **Pop Sequence (Reverse Order)**:
   - **First pop** retrieves `rbx`.
   - **Second pop** retrieves `rax`.

- **Important**: When restoring multiple registers, **pop them in the reverse order** of how they were pushed to maintain data integrity.

### Stack Usage with Functions and Syscalls
- **Purpose**: Stack is often used to save register values when calling **functions** or **syscalls** that may alter those registers.
- **Typical Workflow**:
  - **Push** the values of registers before a function/syscall.
  - Execute the function/syscall.
  - **Pop** the values back to restore the original register values.
- **Example Use Case**: 
  - To preserve `rax` during a syscall, `push rax` before the call and `pop rax` afterward.

#### Code Example: Using Stack with Syscall
```asm
global _start

section .text
_start:
    xor rax, rax       ; initialize rax to 0
    xor rbx, rbx       ; initialize rbx to 0
    inc rbx            ; set rbx to 1
    push rax           ; save rax on the stack
    push rbx           ; save rbx on the stack
    ; syscall or function call
    pop rbx            ; restore rbx from stack
    pop rax            ; restore rax from stack
```

### Example of Stack Behavior in GDB
- **Before Push**:
  - `rax = 0x0`, `rbx = 0x1`
  - Stack (top-to-bottom): `0x0000`, `0x0001`
- **After Push `rax` and `rbx`**:
  - Stack (top-to-bottom): `rbx`, `rax`
- **After Pop `rbx` and `rax`**:
  - Stack restored to initial state, with original values in `rbx` and `rax`.

### Important Considerations
- **Order of Operations**: 
  - When using multiple `push` and `pop` operations, **maintain reverse order** for `pop` to correctly restore registers.
- **Copy Behavior**: 
  - `push` is a copy operation—the original register values remain in the registers even after pushing them onto the stack.
  
### Practical Guidelines
1. **Use `push` and `pop` for Temporary Storage**:
   - Store values temporarily during function/syscall calls to avoid overwriting important data.
2. **Ensure Correct Order**:
   - When pushing multiple values, always pop them in the reverse order to maintain LIFO structure.
3. **Monitor Stack State**:
   - Ensure the top of the stack contains the value you want to pop; avoid accidental overwrites or retrieving incorrect data.

### Summary
- The stack is a vital memory segment used to temporarily store register data.
- **Push/Pop Mechanism**: Simple LIFO structure with `push` (store) and `pop` (retrieve).
- **Use Cases**: Primarily used in function and syscall contexts to protect register data from being altered.
- **Order Matters**: Reverse the order when popping to correctly restore registers.
  
This foundational understanding of the stack will enable effective use of functions and syscalls in assembly programming.

## Questions
- Debug the attached binary to find the flag being pushed to the stack
	- answer