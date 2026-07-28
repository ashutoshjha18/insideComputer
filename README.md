
# This document contains summary of mentioned topics :

---

# Table of Contents

1. Computer Architecture Overview
2. CPU
3. RAM (Main Memory)
4. Memory Hierarchy
5. ROM
6. SSD / HDD
7. Process Memory Layout
8. Code Segment
9. Data Segment
10. BSS Segment
11. Read-Only Data (.rodata)
12. Heap
13. Stack
14. Dynamic Memory
15. Pointers & Memory Addresses
16. CPU Execution Cycle
17. Memory Buses
18. Program Execution Flow
19. Learning Roadmap
20. Key Takeaways

---

# 1. Computer Architecture Overview

A running program moves through several hardware components before the CPU executes it.

```text
SSD/HDD                                            
   │
   ▼
RAM
   │
   ▼
Cache
   │
   ▼
Registers
   │
   ▼
CPU
```

Each level is faster but smaller than the one below it.
 **Basically:**
```text
 Program Stored on SSD
        │
        ▼
Operating System Loads Program
        │
        ▼
RAM (Process Memory)
        │
        ▼
CPU Executes Instructions
```
---

# 2. CPU

Its primary job is to:

* Fetch instructions
* Decode instructions
* Execute instructions

It continuously repeats:

```text
Fetch
   ↓
Decode
   ↓
Execute
   ↓
Repeat
```

The CPU never executes programs directly from the SSD.

---

# 3. RAM (Main Memory)

RAM stands for Random Access Memory.

RAM **is the Main Memory** of the computer.

Characteristics:

* Temporary (Volatile)
* Very Fast
* Stores running programs
* Stores currently used data

When power is removed Everything disappears.

---

# 4. Memory Hierarchy

```text
Fastest
──────────────

Registers

↓

L1 Cache

↓

L2 Cache

↓

L3 Cache

↓

RAM

↓

SSD

↓

HDD

──────────────
Largest
```

---

## Why not use only Cache?

Cache uses SRAM.

SRAM is:

* Faster
* Larger
* Much more expensive

RAM uses DRAM.

DRAM is:

* Slower
* Smaller cells
* Much cheaper
* Can be produced in very large capacities

Therefore, computers combine:

Fast + Small + Expensive

with

Slower + Large + Cheap

instead of using only one memory type.

---

# 5. ROM

ROM (Read Only Memory)

Stores firmware.

**What is Firmware?**

Firmware is software permanently stored on a chip (usually flash memory) on the motherboard.

It is between hardware and the operating system.

Examples:

* BIOS -Basic Input/Output System (old computers use this firmware)
```text
       
       Power Button
          │
          ▼
     BIOS Starts
          │
          ▼
     Checks Hardware
          │
          ▼
    Finds Boot Device
          │
          ▼
    Loads Operating System
          │
          ▼
    Windows Starts
```

* UEFI -Unified Extensible Firmware Interface (modern computers and laptops use this firmware)
```text

                           Power Button
                                 │
                                 ▼
                           UEFI Starts
                                 │
                                 ▼
                           Checks Hardware
                                 │
                                 ▼
                           Loads EFI Boot Manager
                                 │
                                 ▼
                           Loads Windows/Linux
                                 │
                                 ▼
                           Operating System Starts

```
* BIOS and UEFI are both firmware. Their job is to start the computer before the operating system (Windows, Linux, etc.) begins running.

* ROM starts the computer.

Boot sequence:

```text
Power On

↓

CPU

↓

ROM (BIOS/UEFI)

↓

Hardware Check

↓

Load OS from SSD

↓

RAM

↓

CPU executes OS
```

ROM is **not** the SSD.

---

# 6. SSD / HDD

Secondary Storage

Stores:

* Windows
* Linux
* Applications
* Photos
* Videos
* Documents
* Games

Characteristics:

* Permanent
* Large
* Slower than RAM

---

# 7. Process Memory Layout

When a program starts, the operating system loads it into RAM.

**Modern RAM**

```text
High Address
+--------------------------------+
| Command Line Arguments         |
+--------------------------------+
| Stack                          |
| (grows downward)               |
+--------------------------------+
| Free Space                     |
+--------------------------------+
| Heap                           |
| (grows upward)                 |
+--------------------------------+
| BSS Segment                    |
+--------------------------------+
| Data Segment                   |
+--------------------------------+
| Read Only Data (.rodata)       |
+--------------------------------+
| Code/Text Segment              |
+--------------------------------+
Low Address
```
Everything above exists inside RAM.

**old RAM**  

```text           
+----------------------+
| Code Segment         |1000(address)
+----------------------+
| Data Segment         |5000
+----------------------+
| Heap                 |10000
+----------------------+
| Stack                |15000
+----------------------+
```
---

# 8. Code Segment

Stores:

* Machine instructions
* Compiled functions

Example:

```cpp
int add(int a, int b) {
    return a + b;
}
```

Compiled instructions live here.

The CPU fetches instructions from this region.

---

# 9. Data Segment

Stores initialized global and static variables.

Example:

```cpp
int x = 10;
static int y = 20;
```

---

# 10. BSS Segment

Stores uninitialized global and static variables.

Example:

```cpp
int count;
static int total;
```

Automatically initialized to zero.

---

# 11. Read-Only Data (.rodata)

Stores:

* String literals
* Constants

Example:

```cpp
cout << "Hello";
```

The string `"Hello"` is stored in the read-only data segment.

---

# 12. Heap

Heap is used for Dynamic Memory Allocation.

Created using:

```cpp
new
```

or

```cpp
malloc()
```

Example:

```cpp
int* p = new int(50);
```

Memory:

```text
Stack                     Heap

p ----------------------> 50
```

Heap memory remains allocated until released.

C++:

```cpp
delete p;
```

Java:

Garbage Collector releases memory automatically.

---

# 13. Stack

Stack stores:

* Local variables
* Function parameters
* Return addresses
* Function call information

Example:

```cpp
void fun() {
    int x = 5;
}
```

Memory:

```text
Stack

x

↓

Destroyed after function returns
```

Stack memory is managed automatically.

* int* p = new int(50);

```text
Stack                      Heap
┌────────────┐
│ p          │──────────────►┌───────────┐
│ 0x5000     │               │ value=50  │
└────────────┘               └───────────┘
```

---


# 14. Dynamic Memory

Dynamic Memory means memory allocated during program execution (runtime).

Example:

```cpp
Student* s = new Student();
```

The object lives on the heap.

---

# 15. Pointers & Memory Addresses

Every byte in RAM has an address.

Example:

```cpp
int x = 10;
```

Suppose:

```text
Address

15000 → x
```

Pointer:

```cpp
int* p = &x;
```

Stores:

```text
p = 15000
```

Important:

Addresses are not limited to one region.

Pointers can point to:

* Stack
* Heap
* Code Segment
* Data Segment
* Read-Only Data

---

# 16. CPU Execution Cycle

The CPU continuously performs:

```text
Fetch

↓

Decode

↓

Execute
```

Example:

```text
Instruction 1

↓

Instruction 2

↓

Instruction 3

↓

...
```

This cycle happens billions of times every second.

---

# 17. Memory Buses

The CPU communicates with RAM using buses.

### Address Bus

The CPU sends the memory address of the instruction or data it wants.

### Data Bus

RAM sends the requested instruction or data back to the CPU.

### Control Bus

Carries signals such as:

* Read
* Write
* Memory Enable

Overall communication:

```text
CPU
 │
 │ Address Bus
 ▼
RAM

RAM
 │
 │ Data Bus
 ▼
CPU
```

---

# 18. Program Execution Flow

```text
SSD/HDD

↓

Operating System loads Program

↓

RAM

↓

Code Segment

↓

CPU Fetches Instructions

↓

Registers

↓

Instruction Execution
```

The CPU **fetches** instructions from the Code Segment; it does **not** place them there.

---

# 19. Key Takeaways

* RAM **is** the computer's main memory.
* Heap and Stack are logical regions inside RAM.
* The CPU fetches instructions from the Code Segment.
* Registers and Cache are faster than RAM but are much smaller and more expensive.
* ROM stores firmware (BIOS/UEFI), while SSD/HDD stores the operating system, applications, and user files.
* Every location in RAM has an address, and pointers can store addresses that point to the stack, heap, code segment, data segment, or read-only data.
* Understanding memory architecture forms the foundation for learning C++, Java, Operating Systems, Computer Organization, and System Design.

---

**This README will be regularly updated with new topics, real-world examples, and improved visualizations to make it a comprehensive learning resource.**
