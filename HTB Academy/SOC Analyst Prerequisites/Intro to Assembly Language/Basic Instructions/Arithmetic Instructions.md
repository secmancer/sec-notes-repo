## Arithmetic Instructions in x86 Assembly

### Overview
Arithmetic instructions allow for performing **mathematical operations** on data in registers or memory. They can be divided into two types:
- **Unary Instructions**: Operate on a single operand (e.g., increment or decrement).
- **Binary Instructions**: Operate on two operands (e.g., addition or subtraction).

These instructions are processed by the **ALU** (Arithmetic Logic Unit) in the CPU.

---

### 1. Unary Arithmetic Instructions

Unary instructions modify a single operand, typically by **incrementing** or **decrementing** its value. 

| **Instruction** | **Description**             | **Example**                           |
|-----------------|-----------------------------|---------------------------------------|
| `inc`           | Increment by 1              | `inc rax` → `rax += 1` (e.g., 1 to 2)|
| `dec`           | Decrement by 1              | `dec rax` → `rax -= 1` (e.g., 1 to 0)|

#### Example Code
In the **Fibonacci calculator**, initialize `al` and `bl` to 0 and increment `bl`:
```assembly
global _start

section .text
_start:
    mov al, 0      ; Initialize `al` to 0
    mov bl, 0      ; Initialize `bl` to 0
    inc bl         ; Increment `bl` by 1 (now `bl = 1`)
```

---

### 2. Binary Arithmetic Instructions

Binary instructions operate on two operands: a **destination** and a **source**. The result is stored in the destination operand.

| **Instruction** | **Description**                                 | **Example**                                  |
|-----------------|-------------------------------------------------|----------------------------------------------|
| `add`           | Add source to destination                       | `add rax, rbx` → `rax = rax + rbx`          |
| `sub`           | Subtract source from destination                | `sub rax, rbx` → `rax = rax - rbx`          |
| `imul`          | Multiply destination by source                  | `imul rax, rbx` → `rax = rax * rbx`         |

#### Example Code
In the Fibonacci sequence, the **`add`** instruction is essential for calculating the next number in the sequence:
```assembly
global _start

section .text
_start:
    mov al, 0      ; Initialize `al` to 0
    mov bl, 1      ; Initialize `bl` to 1
    add rax, rbx   ; `rax = rax + rbx` (now `rax = 1`)
```

---

### 3. Bitwise Arithmetic Instructions

Bitwise instructions perform **bit-level operations** on data. These are useful for tasks that involve **binary manipulation**.

| **Instruction** | **Description**                                     | **Example**                                    |
|-----------------|-----------------------------------------------------|------------------------------------------------|
| `not`           | Bitwise NOT (invert each bit)                       | `not rax` → `~00000001` = `11111110`          |
| `and`           | Bitwise AND (1 if both bits are 1, else 0)          | `and rax, rbx` → `00000001 & 00000010` = `0`  |
| `or`            | Bitwise OR (1 if any bit is 1)                      | `or rax, rbx` → `00000001 | 00000010` = `3`   |
| `xor`           | Bitwise XOR (1 if bits differ, else 0)              | `xor rax, rbx` → `00000001 ^ 00000010` = `3`  |

#### Common Use Case for `xor`
- **Zeroing a Register**: `xor rax, rax` is a quick way to set `rax` to 0 (by XORing the register with itself).

#### Example Code (Using `xor` for Zeroing)
```assembly
global _start

section .text
_start:
    xor rax, rax   ; Set `rax` to 0
    xor rbx, rbx   ; Set `rbx` to 0
    inc rbx        ; `rbx = 1`
    add rax, rbx   ; `rax = rax + rbx` (now `rax = 1`)
```

This approach is more efficient than using `mov` to load zero, as `xor` produces shorter machine code.

---

### Summary of Key Concepts

- **Unary Instructions** (`inc` and `dec`): Modify a single operand by 1.
- **Binary Instructions** (`add`, `sub`, `imul`): Operate on two operands, with the result stored in the destination.
- **Bitwise Instructions** (`not`, `and`, `or`, `xor`): Perform binary operations on each bit of the operands.
  - `xor` is especially useful for **zeroing registers** efficiently.


## Questions
- Add an instruction to the end of the attached code to "xor" "rbx" with "15". What is the hex value of 'rbx' at the end?
	- answer