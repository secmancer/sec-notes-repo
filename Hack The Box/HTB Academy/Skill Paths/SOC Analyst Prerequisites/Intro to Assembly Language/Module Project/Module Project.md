### Introduction
- So far, we have learned the basics of computer and CPU architecture and the basics of Assembly language and debugging. We will now start learning various x86 assembly instructions. We are likely to run into these types of instructions during penetration testing and reverse engineering exercises, so understanding how they work gives us the ability to interpret what they are doing and understand what the program is doing.
- We will start by learning how to move data and values between registers and memory addresses. Then, we will learn instructions that take one operand (`Unary Operations`) and instructions with two operands ( `Binary Instructions`). Later on, we will go through assembly control instructions and shellcoding.



### Fibonacci Sequence
- Before we start, however, let's discuss the program we will be developing throughout this module, using the various instructions we will learn.  
- `We will be developing a basic Fibonacci sequence calculator using x86 assembly language.`

![fibonacci](https://academy.hackthebox.com/storage/modules/85/fibonacci_sequence.png)

- At the simplest term, a Fibonacci number is the sum of the two numbers preceding it in the sequence (i.e. `F<sub>n</sub> = F<sub>n-1</sub> + F<sub>n-2</sub>`). For example, if we start with `F<sub>0</sub>=0` and `F<sub>1</sub>=1`, then F<sub>2</sub> is `F<sub>1</sub> + F<sub>0</sub>`, which is `F<sub>2</sub> = 1 + 0 -> 1`.  
- Following the same formula, F<sub>3</sub> is `F<sub>3</sub>=1+1=2`, F<sub>4</sub> is `F<sub>4</sub> = 2 + 1 -> 3`, and so on.
- If we continue until F<sub>10</sub>, this is the sequence we would have: `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55`. As we can see, each number equals the sum of the two before it.


### Golden Ratio
- Fibonacci sequence is handy in many fields, like art, mathematics, physics, computer science, and even economics and finance. For example, the Fibonacci sequence is an excellent representation of the golden ratio (`or phi Φ`), which was used by many artists and architects throughout history and seen everywhere around us in nature.

![golden_ratio_examples](https://academy.hackthebox.com/storage/modules/85/golden_ratio_examples_1.jpg)
- Furthermore, many modern designers are using the golden ratio in their designs, most famously in the logos of some known brands.
![golden_ratio_logos](https://academy.hackthebox.com/storage/modules/85/golden_ratio_logos.jpg)
- If you are interested in learning more about the Golden Ratio, you can watch [this video](https://youtu.be/4TF6mMUe3FY).


### Final Program
- We will be developing a Fibonacci sequence calculator for this module, which allows us to practice various assembly instructions as we learn them and build the program as we go until we have the complete calculator program by the end.
- The program will first ask you for the maximum Fibonacci you want to calculate and then print all Fibonacci numbers up to this number. The following example shows us how it would look.
```shell-session
secmancer@htb[/htb]$ ./fib 

Please input max Fn
100
1
1
2
3
5
8
13
21
34
55
89
```
- By the end of the module, you will have developed the above program using nothing but Assembly instructions. We can download the final program from [this link](https://academy.hackthebox.com/storage/modules/85/fib.zip) and run it to see the final project result.