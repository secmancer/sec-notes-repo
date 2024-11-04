## Program Control Instructions: Loops in x86 Assembly

### Overview
Control instructions in assembly language **alter the flow of the program**. Unlike sequential line-by-line execution, control instructions enable features like **loops**, **branching**, and **function calls**. This allows more complex behaviors, such as repeated tasks or conditional logic.

### Loop Structure
A **loop** in assembly repeats a set of instructions for a specified number of times, controlled by the **`rcx` register**. The basic structure of a loop involves:
1. Setting the number of iterations in `rcx`.
2. Using the `loop` instruction, which decrements `rcx` by 1 after each iteration.
3. The loop continues until `rcx` reaches 0.

#### Loop Instructions

| **Instruction** | **Description**                                  | **Example**                     |
|-----------------|--------------------------------------------------|---------------------------------|
| `mov rcx, x`    | Sets the loop counter to `x`                     | `mov rcx, 3`                    |
| `loop label`    | Decrements `rcx` by 1 and jumps to `label` if `rcx` > 0 | `loop exampleLoop`               |

---

### Example Loop Structure

The following code demonstrates a simple loop in assembly:

```assembly
exampleLoop:
    instruction 1
    instruction 2
    loop exampleLoop
```

- **How it works**:
  - The code at `exampleLoop` is executed.
  - **`rcx` is decremented** each time `loop` is called.
  - If `rcx` is not zero, execution jumps back to `exampleLoop`.
  
---

### Fibonacci Sequence with Loops

To automate the calculation of the **Fibonacci sequence**, we can use a loop. The key steps are:
1. **Initialize `rax` and `rbx`**: These registers will hold the current Fibonacci number and the next Fibonacci number, respectively.
2. **Use a loop** to continuously calculate the next Fibonacci number by adding the two previous numbers.
3. **Swap the registers** after each addition using the `xchg` instruction, ensuring `rax` and `rbx` always contain the two most recent Fibonacci numbers.

---

### Fibonacci Sequence Loop Example

```assembly
global _start

section .text
_start:
    xor rax, rax        ; Initialize `rax` to 0 (F0)
    xor rbx, rbx        ; Initialize `rbx` to 0
    inc rbx             ; Set `rbx` to 1 (F1)
    mov rcx, 10         ; Set loop to run 10 times

loopFib:
    add rax, rbx        ; Calculate next Fibonacci number
    xchg rax, rbx       ; Swap `rax` and `rbx` to store the next two numbers
    loop loopFib        ; Repeat until `rcx` becomes 0
```

- **Explanation**:
  - **`xor rax, rax`** initializes `rax` to 0 (first Fibonacci number).
  - **`inc rbx`** sets `rbx` to 1 (second Fibonacci number).
  - **`mov rcx, 10`** sets the loop to iterate 10 times.
  - **`add rax, rbx`** adds the two most recent Fibonacci numbers.
  - **`xchg rax, rbx`** swaps the values of `rax` and `rbx` to keep track of the two most recent Fibonacci numbers.
  - **`loop loopFib`** decrements `rcx` and repeats the loop until `rcx` becomes 0.

---

### Example Output (Using GDB)

The following shows the Fibonacci sequence calculated through multiple iterations of the loop:

1. **Initial State**:
   - `rax = 0` (F0)
   - `rbx = 1` (F1)
   - `rcx = 10` (loop counter)

2. **First Iteration**:
   - `rax = 1`
   - `rbx = 1`
   - `rcx = 9`

3. **Second Iteration**:
   - `rax = 1`
   - `rbx = 2`
   - `rcx = 8`

4. **Subsequent Iterations**:
   - `rax = 2`, `rbx = 3`
   - `rax = 3`, `rbx = 5`
   - `rax = 5`, `rbx = 8`
   - ...
   - **Final Iteration**: `rax = 34`, `rbx = 55`, `rcx = 0`

The loop successfully calculates the Fibonacci numbers as: **0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55**.

---

### Detailed Breakdown of Loop Execution

- **Before Loop**:
  ```assembly
  xor rax, rax   ; Set `rax = 0`
  xor rbx, rbx   ; Set `rbx = 0`
  inc rbx        ; Set `rbx = 1`
  mov rcx, 10    ; Set loop counter to 10 iterations
  ```

- **During Each Loop**:
  - **`add rax, rbx`**: Calculates the next Fibonacci number by adding `rax` (current Fibonacci) and `rbx` (next Fibonacci).
  - **`xchg rax, rbx`**: Swaps the current and next Fibonacci numbers to update them for the next iteration.
  - **`loop loopFib`**: Decrements `rcx` and repeats the loop if `rcx` > 0.

---

### Key Concepts

- **`rcx` Loop Counter**: The **`rcx` register** is used to store the loop counter. It is decremented automatically by the **`loop`** instruction until it reaches zero.
- **Efficient Fibonacci Calculation**: By using `add` and `xchg`, the Fibonacci sequence can be calculated iteratively, storing and updating the last two numbers.
- **Control Flow**: The **`loop`** instruction controls the number of iterations, creating a structured flow of repeated actions.

---

### Conclusion

By leveraging loops, you can efficiently compute the Fibonacci sequence in assembly by:
- **Initializing** the first two Fibonacci numbers (`0` and `1`).
- **Repeating** the process of summing and swapping numbers using a loop.
- **Automating** the calculation for a set number of iterations using the `rcx` register and `loop` instruction.

## Questions
- Edit the attached assembly code to loop the "loop" label 5 times. What is the hex value of "rax" by the end?
	- 0x100000000