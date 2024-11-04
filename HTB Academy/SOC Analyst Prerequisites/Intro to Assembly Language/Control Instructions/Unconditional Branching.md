## Unconditional Branching Notes

### Overview of Branching Instructions
- **Branching Instructions** allow programs to **jump to any point** if a condition is met.
- **Unconditional Branching** (e.g., `jmp` instruction) makes a **jump without conditions**, always moving to a specified location in code.
- Used primarily for **redirecting program flow** to a specific point **without checking any conditions**.

### The `jmp` Instruction
- **Syntax:** `jmp <label>`
  - Example: `jmp loopFib`
- **Functionality**:
  - **Redirects execution** to the given label or address.
  - **Program continues** from the new location without returning automatically.
  - If a temporary jump with a return is needed, **functions** are more appropriate.

### Characteristics of `jmp`
- **Unconditional Jump**:
  - Executes the jump **regardless of any conditions**.
  - Differs from **Conditional Branching**, where jumps occur only if certain conditions are satisfied.

### Example Code: Fibonacci Sequence with `jmp`

#### Assembly Code Sample
```asm
global _start

section .text
_start:
    xor rax, rax    ; initialize rax to 0
    xor rbx, rbx    ; initialize rbx to 0
    inc rbx         ; increment rbx to 1
    mov rcx, 10

loopFib:
    add rax, rbx    ; calculate next Fibonacci number
    xchg rax, rbx   ; swap values
    jmp loopFib     ; jump unconditionally back to loopFib
```

#### Explanation of Code
- **Registers Used**:
  - **`rax`** and **`rbx`**: Hold Fibonacci numbers.
  - **`rcx`**: Initially set to `10` but **not used as a counter** here.
- **Loop Behavior**:
  - `jmp loopFib` creates an **infinite loop**, continuously calculating Fibonacci numbers.
  - The program **does not terminate naturally** since `jmp` repeats the loop without a condition.
  - **No decrement** in `rcx` (unlike in a conditional loop), leading to a continuous, unregulated loop.

### Debugging & Program Flow Observation
- **Using GDB**:
  - Set a **breakpoint** at `loopFib` to observe the program flow.
  - **Output** shows Fibonacci sequence in registers `rax` and `rbx`.
  - **Uninterrupted Loop**: Program runs indefinitely, displaying higher Fibonacci values with each iteration.

### Key Observations
- **Infinite Loop Behavior**:
  - Without a condition to stop `jmp`, the loop **runs endlessly**.
  - This can be compared to a **`while true`** loop in high-level languages.
- **Program Termination**:
  - Manually stopped with **`ctrl+c`** due to endless execution.
  - Final values in registers (e.g., `rax`, `rbx`) show **large Fibonacci numbers** due to continual accumulation.

### Use Cases for `jmp`
- **Best for Situations Requiring Constant Redirection**:
  - Situations where continuous jumps are required **without checking conditions**.
  - **Not ideal for loops** requiring a termination condition, as it can lead to infinite loops.

### Limitations of Unconditional `jmp`
- **Cannot control loop iterations** directly since no condition checks.
- **Better suited for**:
  - **Simple, unconditional redirections**.
  - Situations where **conditional checks** are not needed or handled externally.

### Transition to Conditional Branching
- **Conditional Branching** will be used to **control jump behavior** by adding conditions, which **prevents infinite looping**.
- **Next Step**: Explore how **Conditional Branching** provides more control over program flow by allowing jumps only if specific criteria are met.

## Questions
- Try to jump to "func" before "loop loop". What is the hex value of "rbx" at the end?
	- 0x4