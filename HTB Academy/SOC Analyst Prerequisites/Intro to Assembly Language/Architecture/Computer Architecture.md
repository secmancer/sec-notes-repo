## Computer Architecture Notes

### **Overview of Von Neumann Architecture**
- **Developed in 1945** by John Von Neumann for **general-purpose computers**.
- Inspired by **Alan Turing's** ideas and **Charles Babbage's** concept of a **programmable computer**.
- **Core components**:
  - **CPU (Central Processing Unit)** 
  - **Memory Unit**
  - **Input/Output (I/O) Devices**:
    - **Mass Storage Unit**
    - **Keyboard**
    - **Display**
  
- **CPU components**:
  - **Control Unit (CU)**
  - **Arithmetic/Logic Unit (ALU)**
  - **Registers**

- Still used in **modern computers**, servers, and smartphones.

### **Importance in Assembly Language and Exploitation**
- **Assembly language** interacts primarily with the **CPU** and **memory**.
- Understanding **computer architecture** is crucial for optimizing performance in assembly and for **binary exploitation** (e.g., stack overflows, ROP, heap exploits).

---

### **Memory**
- Memory stores temporary **data** and **instructions** for running programs.
- It is a **primary location** for the CPU to access data and must be **fast** for efficient processing.
  
#### **Types of Memory**:
1. **Cache Memory** (inside CPU):
   - **Extremely fast** but **limited** in size.
   - Divided into three levels based on proximity to the CPU:
     - **L1 Cache**: Fastest, located in each CPU core (typically in kilobytes).
     - **L2 Cache**: Shared between CPU cores, larger and slightly slower than L1.
     - **L3 Cache**: Larger but slower than L1 and L2, not present in all CPUs.
  
2. **Random Access Memory (RAM)**:
   - Larger than cache memory (in **gigabytes** or **terabytes**).
   - **Slower** than cache memory and located **far from the CPU**.
   - Critical for storing program data and instructions.
   
   **Memory Access Times**:
   - **Registers**: 1 clock cycle
   - **L1 Cache**: A few cycles
   - **RAM**: ~200 clock cycles

#### **Memory Segments in RAM**:
- **Stack**: Fixed size, follows **Last-in, First-out (LIFO)** order.
- **Heap**: Larger and versatile, stores data in **non-sequential order** (slower than Stack).
- **Data**:
  - **Data Segment**: Holds variables.
  - **.bss Segment**: Holds uninitialized variables.
- **Text**: Contains **assembly instructions** for execution.

---

### **Input/Output (I/O) and Storage**
- **I/O Devices** include the **keyboard**, **screen**, and **mass storage**.
- CPU accesses I/O devices and memory using **Bus Interfaces**:
  - Buses transfer data in parallel, typically in multiples of **4-bits**, up to **128-bits**.
  - Buses connect CPU with **external components**.

#### **Storage (Secondary Memory)**:
- **Permanent storage** for data and programs (e.g., operating system, applications).
- **Slower** than RAM, accessed through interfaces like **SATA** or **USB**.
  
#### **Types of Storage**:
- **Hard Disk Drives (HDD)**: Older, magnetic storage technology.
- **Solid-State Drives (SSD)**: Faster, non-volatile memory, similar to RAM but retains data without power.

---

### **Memory and Storage Speed Hierarchy**
| **Component** | **Speed** | **Size** |
|---------------|-----------|----------|
| **Registers** | Fastest   | Bytes    |
| **L1 Cache**  | Fastest (after Registers) | Kilobytes |
| **L2 Cache**  | Very fast | Megabytes |
| **L3 Cache**  | Fast, slower than L1/L2 | Megabytes |
| **RAM**       | Slower than Cache | Gigabytes-Terabytes |
| **Storage**   | Slowest   | Terabytes and beyond |

- **Speed vs Size**: The closer a component is to the **CPU core**, the faster but smaller it is.