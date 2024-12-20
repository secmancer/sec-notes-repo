### Introduction
- **High-Level vs. Low-Level Languages**: Applications on personal computers and smartphones are typically developed using high-level languages (e.g., C++, Java, Python).
- However, processors only understand binary (`1`s and `0`s).
- **Role of Assembly Language**: Assembly serves as a low-level language that provides human-readable machine instructions, which can be converted into binary code for the processor to execute. 
- It bridges the gap between high-level programming and machine code.
- **Symbolic Machine Code**: Assembly is often called symbolic machine code because its syntax (e.g., `add rax, 1`) is more intuitive than machine code (`4883C001`) or binary (`01001000 10000011 11000000 00000001`).
- **Machine Code and Shellcode**: Machine code, often referred to as shellcode, is the hexadecimal representation of machine instructions. 
- Shellcode can be translated back to Assembly or executed directly as binary instructions loaded into memory.



### High-level vs. Low-level
- **Processor-Specific Assembly**: Different processor designs require unique sets of machine instructions and Assembly languages, making it historically challenging to develop applications for multiple processors.
- **High-Level Languages and Compilers**: The development of high-level languages like `C` in the 1970s allowed developers to write processor-independent code.
- Compilers translate high-level code into processor-specific assembly and machine code.
- **Interpreted Languages**: Languages like `Python`, `PHP`, and `JavaScript` are not compiled but interpreted at runtime. 
- They rely on pre-built libraries, often written in languages like `C` or `C++`, which execute commands using processor-specific assembly and machine code.
- **Libraries in Interpreted Languages**: When a command is issued in an interpreted language, the associated library's compiled code performs the necessary operations on the processor, bridging the gap between high-level commands and low-level execution.



### Compilation Stages
![Compilation Stages](https://academy.hackthebox.com/storage/modules/85/assembly_Compilation_Stages_1.jpg)
- Let's take a basic '`Hello World!`' program that prints these words on the screen and show how it changes from high-level to machine code.
- In an interpreted language, like Python, it would be the following basic line.
```python
print("Hello World!")
```

- If we run this Python line, it would be essentially executing the following `C` code.
```c
#include <unistd.h>

int main()
{
    write(1, "Hello World!", 12);
    _exit(0);
}
```
- Note: the actual `C` source code is much longer, but the above is the essence of how the string '`Hello World!`' is printed. 
- If you are ever interested in knowing more, you can check out the source code of the Python3 print function at this [link](https://github.com/python/cpython/blob/0332e569c12d3dc97171546c6dc10e42c27de34b/Python/bltinmodule.c#L1829) and this [link](https://github.com/python/cpython/blob/9975cc5008c795e069ce11e2dbed2110cc12e74e/Objects/fileobject.c#L119)
- The above `C` code uses the Linux `write` syscall, built-in for processes to write to the screen.
```nasm
mov rax, 1
mov rdi, 1
mov rsi, message
mov rdx, 12
syscall

mov rax, 60
mov rdi, 0
syscall
```

- As we can see, when the `write` syscall is called in `C` or Assembly, both are using `1`, the text, and `12` as the arguments. 
- This will be covered more in-depth later in the module.
- From this point, Assembly code, shellcode, and binary machine code are mostly identical but written in different formats.
```shellcode
48 c7 c0 01
48 c7 c7 01
48 8b 34 25
48 c7 c2 0d
0f 05

48 c7 c0 3c
48 c7 c7 00
0f 05
```
- Finally, for the processor to execute the instructions linked to this machine, it would have to be translated into binary.
```binary
01001000 11000111 11000000 00000001
01001000 11000111 11000111 00000001
01001000 10001011 00110100 00100101
01001000 11000111 11000010 00001101 
00001111 00000101

01001000 11000111 11000000 00111100 
01001000 11000111 11000111 00000000 
00001111 00000101
```
- A CPU uses different electrical charges for a `1` and a `0`, and hence can calculate these instructions from the binary data once it receives them.
- Note: With multi-platform languages, like `Java`, the code is compiled into a Java Bytecode, which is the same for all processors/systems, and is then compiled to machine code by the local Java Runtime environment. 
- This is what makes Java relatively slower than other languages like C++ that compile directly into machine code. Languages like C++ are more suitable for processor intensive applications like games.
- We now see how computer languages progressed from assembly language unique for each processor to high-level languages that can work on any device without even needing to be compiled.



### Value for Pentesters
- Assembly language is essential for binary exploitation, a critical aspect of penetration testing, enabling the disassembly, debugging, and analysis of binary instructions in memory to find vulnerabilities.
- Binary exploitation techniques, such as buffer overflows, ROP chains, and heap exploitation, require understanding assembly instructions and creating custom exploits with shellcode.
- Knowledge of Intel x86 Assembly is vital for writing exploits for modern binaries, while ARM Assembly is increasingly relevant for modern devices like smartphones and ARM-based laptops.
- Although this module focuses on Intel x86 Assembly, its foundational concepts are helpful for learning ARM Assembly due to their similarities.



### Optional Exercises
- In the above 'Hello World' example, which Assembly instruction will '00001111 00000101' execute?
	- syscall