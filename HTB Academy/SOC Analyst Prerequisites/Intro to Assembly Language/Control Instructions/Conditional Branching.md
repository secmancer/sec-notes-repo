## Notes on Conditional Branching in Assembly

### Overview
- **Conditional Branching Instructions** enable program control flow to change **only when specific conditions are met**.
- These instructions rely on **condition codes (Jcc)**, where `cc` represents a specific condition.
- Conditional jumps are more versatile than unconditional jumps, allowing targeted execution control.

### Common Conditional Jump Instructions (Jcc)
| **Instruction** | **Condition**       | **Description**                             |
|-----------------|---------------------|---------------------------------------------|
| `jz`            | D = 0               | Jump if Destination is Zero                |
| `jnz`           | D ≠ 0               | Jump if Destination is Not Zero            |
| `js`            | D < 0               | Jump if Destination is Negative            |
| `jns`           | D ≥ 0               | Jump if Destination is Not Negative        |
| `jg`            | D > S               | Jump if Destination is Greater than Source |
| `jge`           | D ≥ S               | Jump if Destination is Greater or Equal to Source |
| `jl`            | D < S               | Jump if Destination is Less than Source    |
| `jle`           | D ≤ S               | Jump if Destination is Less or Equal to Source |

- **Note**: Full list of condition codes available in the Intel x86_64 manual.

### Conditional Movements (`CMOVcc` and `SETcc`)
- Conditional instructions apply to more than just jumps.
- **`CMOVcc`**: Conditional move, such as `cmovz rax, rbx` (moves `rbx` to `rax` if condition is zero).
- **`SETcc`**: Conditional set, such as `setz rax` (sets byte in `rax` to `1` if zero, otherwise `0`).

### RFLAGS Register and Condition Flags
- **RFLAGS Register** stores various flag bits, updated based on the result of the last instruction.
- Key **flags**:
  - **Zero Flag (ZF)**: Set to `1` if result is zero.
  - **Sign Flag (SF)**: Set if result is negative.
  - **Carry Flag (CF)**: Indicates carry/borrow in operations.
  - **Parity Flag (PF)**: Set based on the parity (even/odd) of the result.

#### Example Flag Usage:
- `jnz` uses **ZF**: Jumps if **ZF is `0`** (i.e., result was non-zero).
- **Flags in RFLAGS**:
  - Common flags: **CF, ZF, SF, PF**.
  - **Zero Flag (ZF)**: Determines if the last result was zero.
  - **Sign Flag (SF)**: Indicates if the result was negative.

### Example of Conditional Branching: Fibonacci Sequence

#### Code Example Using `jnz` for Loop Control
```asm
global _start

section .text
_start:
    xor rax, rax       ; initialize rax to 0
    xor rbx, rbx       ; initialize rbx to 0
    inc rbx            ; set rbx to 1
    mov rcx, 10        ; set loop counter to 10
loopFib:
    add rax, rbx       ; calculate next Fibonacci number
    xchg rax, rbx      ; swap rax and rbx
    dec rcx            ; decrement rcx
    jnz loopFib        ; jump back to loopFib until rcx reaches 0
```
- **Explanation**:
  - The `dec rcx` and `jnz loopFib` loop until `rcx` becomes `0`.
  - When `rcx` reaches `0`, **ZF** is set, preventing `jnz` from jumping again.

### `cmp` Instruction for Conditional Comparisons
- **`cmp`**: Compares two operands by performing subtraction (D - S) and updating flags without storing the result.
  - Example: `cmp rbx, 10`
    - Performs `rbx - 10`, updating flags based on the outcome.

#### Code Example Using `cmp` and `js` for Conditional Looping
```asm
global _start

section .text
_start:
    xor rax, rax       ; initialize rax to 0
    xor rbx, rbx       ; initialize rbx to 0
    inc rbx            ; set rbx to 1
loopFib:
    add rax, rbx       ; calculate next Fibonacci number
    xchg rax, rbx      ; swap rax and rbx
    cmp rbx, 10        ; compare rbx to 10
    js loopFib         ; jump to loopFib if rbx < 10 (SF = 1)
```
- **Explanation**:
  - `cmp rbx, 10` sets flags based on whether `rbx` is less than `10`.
  - `js loopFib` jumps only if **Sign Flag (SF)** is set (i.e., result is negative).

### GDB Debugging Tips for Conditional Branching
- **Setting Conditional Breakpoints**:
  - Example: `b *loopFib+9 if $rbx > 10` sets a breakpoint at `js loopFib` when `rbx > 10`.
  - Use `disas` to find exact instruction addresses for setting precise breakpoints.

#### Observing Flag Behavior in GDB
- **GEF Plugin**: Displays **RFLAGS** state, showing which flags are set after instructions.
- **Example**:
  - `js loopFib` taken if **SF** is set; otherwise, GEF displays `NOT taken`.

### Comparison of Control Flow Methods
| **Method**                           | **Description**                                               |
|--------------------------------------|---------------------------------------------------------------|
| `loop loopFib`                       | Uses `loop` to repeat 10 times based on `rcx` counter.        |
| `dec rcx` + `jnz loopFib`            | Decrements `rcx` and jumps if `rcx` is not zero.              |
| `cmp rbx, 10` + `js loopFib`         | Uses `cmp` and `js` to loop while `rbx < 10`.                 |

- **Efficiency**:
  - `loop` instruction is compact but less flexible than `cmp` + `js`.
  - **`cmp` + `js`** offers more control, as it can handle custom conditions beyond counters.

### Summary
- **Conditional Branching** (Jcc instructions) allow jumps based on conditions set in **RFLAGS**.
- **RFLAGS** flags, especially **ZF, SF, CF**, play a central role in conditional operations.
- **`cmp` and conditional jumps** enable complex decision-making without altering operands.
- Conditional branching increases code flexibility and control, essential for advanced program flow.

## Questions
- The attached assembly code loops forever. Try to modify (mov rax, 5) to make it not loop. What hex value prevents the loop?
	- 0x2