## Reverse Engineering
- “Reverse engineering (also known as backwards engineering or back engineering) is a process or method through which one attempts to understand through deductive reasoning how a previously made device, process, system, or piece of software accomplishes a task with very little (if any) insight into exactly how it does so.” (from Wikipedia)
- Figuring out how something works by messing around with it

## Reverse Engineering in CTFs
- Given a thing
	- Usually a binary, usually for Linux, usually for x86_64
	- Can also be a firmware dump, obfuscated script, etc.
- Figure out what it does
- Get the flag
	- Sometimes contained within the thing you're given
	- Sometimes obtainable by connecting to the program running on a remote server

## What we'll be focusing on
- You’re given an x86_64 Linux binary, and you have to figure out what it does
	- Sometimes it’s a “flag checker,” sometimes that program has a “print flag” function that you have to figure out how to trigger on a remote server

## x86_64
- 64-bit ISA
- Very popular in computers*
- Kind of a mess
	- Variable-length instructions
	- 32-bit backwards compatibility
	- What's it even really called (AMD64, x64, x86_64)??

## What the heck is an ISA
- Your computer has a CPU
- CPUs run machine code
- Machine code is made up of instructions
- The instruction set architecture defines what instructions are run
- Also contains a bunch of “registers” (think of them like variables)
	- RSP, RBP, RDX RAX, RBX, R1-R12, etc.
	- Can also use parts of registers as psuedo-registers (for 32-bit and 16-bit backwards compatibility)

## How this process looks
- https://godbolt.org/z/TWffYzf7h

## Memory
![[Screenshot_20241115_221237.png]]

## Program (.text, .data, .rodata, etc.)
- Literally the file, as read from your disk
- Starts executing at the beginning of the .text section (the code)
- File format: generally ELF
	- Contains a bunch of different sections
	- .text, .data
- Tells the OS what libraries it wants to load

![[Screenshot_20241115_221350.png]]

## The Stack (Data Structure)
- FIrst in, last out data structure
- Push: add something to the top of the stack
- Pop: remove the last element from the top of the stack (and return it)
- Peek: looking at the top of the stack, without doing anything to it

## The Stack (for programs)
- Programs start with an "entry" function
- Functions call other functions
- Each function has its own local variables, which need to remain set even after another function is called
	- We store these on the stack!

## The Stack (in x86_64)
- Order (from newest to oldest or lowest in memory to highest in memory)
	- Local variable(s)
	- Saved base pointer (goes into RBP register)
	- Return pointer

## Base Pointer/Frame Pointer
 - The first (meaning highest) address in linear memory where the currently executing function’s local variables are stored.
 - All variables stored on the stack are relative to the base pointer
- E.g. if you have 4-byte variables
	- Variable 1 stored at [RBP-8] (assuming an 8-byte integer)
	- Variable 2 stored at [RBP-16]
	- Etc.

## Stack Pointer
- Register (RSP)
- Set to the top used space on the stack
- When something is pushed to the stack, this is decremented (remember, the stack grows down) by the size of the local variables

## Return Pointer
- When a function returns, the program resumes executing from wherever the function is called
- Functions need to know where to jump back to
- This is stored on the stack

![[Screenshot_20241115_221933.png]]
![[Screenshot_20241115_222040.png]]

## Back to the compiler output...
- https://godbolt.org/z/TWffYzf7h

## Reverse Engineering Tools
- Disassemblers
	- Machine code to assembly
- Decompilers
	- Machine code / assembly to more readable language (like C)
	- Note: machine code generally does not contain sufficient information (e.g. variable names) to fully reconstruct the original program
- Debuggers
	- See how a program works while it's actually executing

## Ghidra
- Free and open-source decompiler
- Made by the NSA
- Download from the NSA website / GitHub and run the "ghidraRun" script
	- Extract the Ghidra zip file
	- Open the new folder in a command prompt
	- Run "./ghidraRun" (or ghidraRun.bat if in Windows)

## GDB
- GNU Debugger
- Can poke around stuff
- "pwndgb" extension makes it better suited for reverse engineering/binary exploitation

## strings
- Literally just finds readable strings in a file
- Very useful actually in certain situations


## strace
- Logs system calls that a program makes


## angr
- Almost magical tool that allows you to find what program input results in a defined program behavior
	- E.g. find input for a given output, or find input for reaching a certain instruction in memory, etc.
- Write scripts in Python


## ...and a whole lot more tools
- radare2/rizin
- Cutter
- IDA Pro
- objdump
- readelf
- etc.

## Using Linux
- Since most reverse engineering problems are distributed as x86_64 Linux ELFs, it’s useful to have a Linux VM
- Windows
	- Search for PowerShell
	- Run as administrator
	- Run the command: "wsl --install"
	- Install tools using "apt install"
		- "sudo apt install gdb build-essential"
- Mac
	- https://tinyurl.com/mac-ctf-vm <- has these tools built into it

## Recommended Problems
- File-run1 / File-run2
- GDB Test Drive
- Reverse
- ASCII FTW
- Bit-O-Asm-1/2/3/4
- GDB Baby Step 1/2/3/4
- bbbbloat