Welcome to this comprehensive study session covering the entire curriculum of **System Fundamentals**. We will explore the theoretical backbone of computer architecture, the practical challenges of operating system design, and advanced topics in concurrency and parallelism, organized across the six modules specified in your syllabus.

---

# Module 1: Introduction to System Fundamentals & Operating System Architecture

Module 1 introduces the core concepts of how computers are organized, how information is represented digitally, and the essential role of the Operating System (OS).

## 1.1 Computer Architecture and Data Representation

### Von Neumann Model
The structure of modern computers often follows the **Von Neumann model**, featuring a Central Processing Unit (CPU) connected to Main Memory and an Input/Output system via interconnections for address, data, and instructions.

### Information Representation
Information within a system is broadly categorized into **Data** and **Program** (coded instruction). Data itself can be:
1.  **Numeric Data:** Including integers (unsigned and signed) and **Floating Point** (often represented using the IEEE 754 format).
2.  **Non-Numeric Data:** Such as ASCII characters.

#### Fixed Point Representation
In fixed point representation, an arbitrary binary point is implied, which divides an $N$-bit field into an integer part and a fractional part.

#### Floating Point Representation (IEEE 754)
The **IEEE 754 Floating-Point Standard** (e.g., 32-bit Single Precision) reserves specific fields for a binary number:
*   **Sign Bit** (1 bit): 0 for positive, 1 for negative.
*   **Exponent** (e.g., 8 bits for single precision).
*   **Mantissa** (e.g., 23 bits for single precision).
To represent a number, one must determine the **True Exponent (TE)**, calculate the **Biased Exponent (BE)** using the formula $\text{BE} = \text{TE} + \text{Bias}$ (where Bias is typically 127 for single precision), and convert the Mantissa into its normalized form.

#### Floating Point Arithmetic
Arithmetic operations, such as addition, require several steps:
1.  Extract the exponent and mantissa bits.
2.  Compare the exponents ($\text{E}_x$ and $\text{E}_y$) to find the difference ($\text{E}_d$).
3.  Shift the mantissa of the smaller number to the right by $\text{E}_d$ times.
4.  Add the aligned mantissas ($\text{M}_x + \text{M}_y$).
5.  Normalize the result and adjust the exponent if necessary, and finally, round the result.

### Microoperations and Arithmetic Units
**Microoperations** are the elemental operations performed on information stored within registers, such as shift, clear, and load. They fall into four primary categories:
1.  **Register Transfer:** Moving binary information from one register to another (e.g., $R2 \leftarrow R1$). Key registers include the Memory Address Register (MAR) and Program Counter (PC).
2.  **Arithmetic:** Basic operations like addition, subtraction, increment, and decrement. Subtraction is commonly implemented using complementation and addition ($R3 \leftarrow R1 + \overline{R2} + 1$).
3.  **Logic:** Operations for bit manipulation on non-numeric data.
4.  **Shift:** Operations including logical shift-left ($\text{shl}$), shift-right ($\text{shr}$), circular shift (rotate, $\text{cil}$, $\text{cir}$), and **Arithmetic Shift** ($\text{ashl}$, $\text{ashr}$). Arithmetic shifts are crucial as shifting left multiplies by $2$ and shifting right divides by $2$, while preserving the sign bit.

### Multiplication and Division Algorithms
The syllabus covers algorithms like the **Booth Multiplication Algorithm** (for signed binary multiplication) and the **Restoring/Non-Restoring Division Algorithms**. These algorithms are iterative procedures relying heavily on microoperations like shifting, adding, and subtracting.

## 1.2 Operating System (OS) Architecture

### Definition and Core Functions
The **Operating System** is software that acts as a program controlling the execution of application programs and serves as the interface between applications and hardware. It is essentially a **Resource Manager**, responsible for managing resources used for moving, storing, and processing data.

The main functions of an OS include:
*   **Memory Management:** Tracking free and used space in Main Memory, allocating/deallocating memory based on process size, and managing process swap In/Out in virtual memory.
*   **Process Management:** Deciding which process is executed first and for how long, and handling different levels of scheduling (Long/Short/Mid term Scheduling).
*   **Device Management:** Allocating and deallocating devices, buffering the information stream, and performing Disk Scheduling.
*   **File Management:** Organizing files, managing access control, and storing file information (name, size, access rights).
*   **Security:** Preventing unauthorized access, often via password protection.

### Operating System Services
The OS offers services to the user and processes, such as:
*   **Program Execution:** Loading instructions/data into memory and performing necessary initialization.
*   **I/O Operation:** Providing a uniform interface for initiating and managing I/O operations, hiding the specific instructions required by individual devices.
*   **File System Manipulation:** Providing controlled access to files, creating, managing, and maintaining file structures, and offering protection mechanisms in multi-user systems.
*   **Error Handling (Detection and Response):** Detecting and responding to internal (memory errors, device failure) or external (division by zero, illegal memory access) errors, and clearing the condition with minimal impact.
*   **Accounting:** Collecting usage statistics and monitoring performance parameters (like response time) for potential system improvement or billing purposes.
*   **Communication:** Enabling communication between processes of the same user or different users.

### Evolution and Types of Operating Systems
OS evolved through several stages to maximize processor utilization:
1.  **Serial Processing:** Programmers interacted directly with hardware, leading to scheduling and setup time problems.
2.  **Simple Batch Systems:** Introduced the concept of the **Monitor** program (executing in **Kernel Mode** to use privileged instructions) to process jobs in batches, improving utilization despite the overhead introduced by the monitor.
3.  **Multiprogrammed Batch Systems:** Solved the problem of the CPU being idle during slow I/O operations by holding multiple programs in memory (multitasking). When one job waits for I/O, the processor switches to another job.
4.  **Time-Sharing Systems:** Extended multiprogramming to handle multiple *interactive* jobs concurrently by sharing processor time among users in short bursts or quanta.

Advanced systems include:
*   **Parallel Operating Systems:** Tightly coupled systems where multiple processors share a single system-wide primary memory address space, focusing on speedup for complex tasks.
*   **Multiprocessor OS:** Must handle additional issues over standard multiprogramming, especially concerning **Synchronization** and **Scheduling** of simultaneous concurrent processes/threads, and managing shared physical pages.
*   **Distributed Operating System:** Loosely coupled systems where applications run across multiple interconnected computers, prioritizing enhanced communication and integration.

### System Calls and Linux Fundamentals

**System Calls** provide the programming interface that connects user applications to OS services. They are usually accessed via high-level **APIs** (like Win32 or POSIX) rather than direct system calls. The API hides implementation details, while the system-call interface uses a numerical index to invoke the appropriate kernel function.

Linux often utilizes a **shell** (like **bash**) for command-line interaction, which many sophisticated users prefer due to its speed, power, and extensibility. When a command is typed, the shell searches for and executes the corresponding program, suspending itself until termination.

File security is managed via permissions, which can be modified using the **`chmod`** command, following the syntax: $\text{chmod } [\text{reference}][\text{operator}][\text{mode}] \text{ file...}$.
*   **Reference Classes** specify who is affected: $\text{u}$ (owner), $\text{g}$ (group), $\text{o}$ (other), or $\text{a}$ (all).
*   **Operators** include $+$ (add mode), $-$ (remove mode), or $=$ (set exact mode).
*   **Permissions (Modes)** are $\text{r}$ (read), $\text{w}$ (write/delete), and $\text{x}$ (execute/search).

---

# Module 2: Central Processing Unit & Process Management

Module 2 details the core structure of the CPU, how it handles instruction flow, and how the operating system manages running processes.

## 2.1 Process Management

### Process Concept and PCB
A **Process** is an active entity, defined as a program in execution, created when an executable file is loaded into memory. One program can generate several processes. The OS manages each process using a **Process Control Block (PCB)**, which contains all necessary information to control and later resume a process, including its identifier, state, priority, program counter, and I/O status.

### Process States
As a process executes, it transitions between states, commonly defined in the Five-State Process Model:
*   **New:** Being created.
*   **Ready:** Waiting for CPU time (admitted from New state).
*   **Running:** Instructions are being executed (dispatched from Ready state).
*   **Blocked/Waiting:** Waiting for an event (e.g., I/O completion) to occur.
*   **Terminated/Exit:** Finished execution (released from Running state).

**Context Switching** is the mechanism where the OS interrupts one running process ($\text{P}_0$), saves its state into its PCB, and reloads the state from another process's PCB ($\text{P}_1$) to allow $\text{P}_1$ to execute.

### Threads
A **Thread** (or **Light Weight Process**) is the basic unit of CPU utilization, consisting of a program counter, a stack, and a set of registers. Threads offer several advantages:
*   **Responsiveness:** Allowing a program to continue even if part of it is blocked.
*   **Resource Sharing:** Threads within the same process run in the same address space and share code and data.
*   **Utilization of Multiprocessor Architecture**.

## 2.2 Instruction Format and Addressing Modes

### Instruction Format
**Machine instructions** are binary codes that determine the operation of the computer system. Each instruction contains specific **information fields** necessary for execution, called **elements of instruction**, typically including:
1.  **Operation Code (Opcode):** Specifies the binary code for the operation.
2.  **Source Operand Address:** Specifies one or more source operands.
3.  **Destination Operand Address:** Specifies where the result of the operation is stored.

Instructions are categorized based on the number of addresses they contain: Zero, One, Two, or Three Address Instructions.

### Addressing Modes
**Addressing modes** specify the mechanism used for locating operands. The most common addressing techniques are:

| Mode | Description | Effective Address (EA) / Operand Access |
| :--- | :--- | :--- |
| **Immediate** | The operand value is contained within the instruction itself. No memory reference is required other than instruction fetch. | $\text{OPERAND} = \text{A}$ (Address Field). |
| **Direct** | The address field (A) contains the effective address (EA) of the operand. | $\text{EA} = \text{A}$. |
| **Indirect** | The instruction contains the address (A) of a memory location that holds the effective address of the operand. | $\text{EA} = (\text{A})$. |
| **Register** | The instruction specifies the address/name of the CPU register (R) containing the operand. | $\text{EA} = \text{R}$. |
| **Register Indirect** | The register (R) specified in the instruction holds the effective address of the operand. | $\text{EA} = (\text{R})$. |
| **Displacement** | Combines the address field (A) with the contents of a register (R). This is used for Relative addressing (R is PC), Base-register addressing, and Indexing. | $\text{EA} = \text{A} + (\text{R})$. |
| **Stack** | Operands are implicitly referenced from the top of the stack, maintained by a stack pointer register (a form of implied addressing). | $\text{PUSH/POP}$ operations. |

## 2.3 Processor Scheduling

**Processor Scheduling** assigns CPU time to processes/threads to meet objectives such as throughput and response time. There are three types of scheduling:
1.  **Long-term scheduling (Admission Scheduler):** Decides which jobs are admitted to the ready queue.
2.  **Mid-term scheduling (Swapper):** Removes/swaps processes from main memory to secondary memory, or vice versa.
3.  **Short-term scheduling (CPU Dispatcher):** Selects which ready, in-memory process executes next; this executes most frequently.

Scheduling employs two modes of operation:
1.  **Non-Preemptive:** Once a process is in the running state, it executes until it voluntarily terminates.
2.  **Preemptive:** The currently running process may be involuntarily interrupted and moved back to the ready state.

Key Scheduling Algorithms include:
*   **Non-Preemptive:** First Come First Serve (FCFS), Shortest Job First (SJF), and Priority.
*   **Preemptive:** Shortest Remaining Time First (SRTF, a preemptive version of SJF), Round Robin (RR), and Preemptive Priority.

Performance is evaluated using metrics such as **Turn Around Time** (submission to completion), **Waiting Time** (time spent in the waiting queue), **Response Time** (submission to first response), **Throughput** (processes completed per unit time), and **CPU Utilization** (keeping the CPU busy).

---

# Module 3: Memory Organization & Memory Management

Module 3 focuses on the hierarchy of storage systems and the techniques the OS uses to manage the limited main memory efficiently.

## 3.1 Memory Hierarchy and Requirements

### Memory Hierarchy
The memory hierarchy organizes all storage devices based on speed, cost, and capacity:
1.  **Register Memory** (Highest speed).
2.  **Cache Memory:** Small, fast memory storing currently executed program data, bridging the speed gap between the CPU and main memory. The access time ratio between cache and main memory is approximately 1 to $7\sim 10$.
3.  **Main Memory (RAM):** Primary memory, volatile, communicating directly with the CPU.
4.  **Auxiliary Memory (Magnetic Disks, Tapes):** Secondary memory, non-volatile, used for permanent storage and swapping programs in and out of main memory.

Main memory is typically faster but volatile (loses data on power failure), whereas secondary memory is non-volatile (retains data) and slower.

### Memory Management Requirements
Effective memory management must satisfy several requirements:
1.  **Relocation:** Since a program's physical memory location is unknown until runtime, and processes are frequently swapped in and out, the OS must be able to **relocate** processes to different memory areas.
2.  **Protection:** Memory references must be checked at run time to ensure a process only accesses locations within its own process image.
3.  **Sharing:** The OS must allow controlled access to shared code (like program copies) by multiple processes without compromising protection, often supported by relocation mechanisms.
4.  **Logical Organization:** Programs are naturally segmented (modules, subroutines). **Segmentation** attempts to manage memory in units corresponding to this logical structure.
5.  **Physical Organization:** Addressing the two-level storage structure (fast, volatile main memory and slow, non-volatile secondary storage).

## 3.2 Memory Partitioning and Allocation

Memory management brings processes into main memory, using techniques like partitioning.

### Contiguous Allocation
This allocates a single, contiguous block of memory to each process.
*   **Fixed Partitioning:** Divides memory into fixed-size, static partitions (either equal or unequal sizes). The primary drawback is **Internal Fragmentation** (wasted space within a partition if the program is smaller than the partition size), and limits the maximum number of active processes.
*   **Dynamic Partitioning:** Uses partitions of variable length, allocated precisely to the process size. This eliminates internal fragmentation but causes **External Fragmentation** (memory broken into many small, unusable blocks of free space). To counter external fragmentation, **Compaction** (shifting processes to consolidate free space) is necessary, though it is time-consuming.

### Placement Algorithms
These algorithms determine which available free block is chosen for a new process request:
*   **First-fit:** Scans memory from the beginning (or last placement location for Next-fit) and selects the first available block large enough for the request.
*   **Best-fit:** Selects the smallest available block whose size is closest to the size requested.
*   **Worst-fit:** (Mentioned as an allocation strategy).

## 3.3 Non-Contiguous Allocation

### Paging
**Paging** solves fragmentation issues by dividing the process (logical memory) into fixed-size **pages**, and physical memory into fixed-size **frames**.
*   The CPU generates a logical address split into a **Page number ($\text{p}$)**, used as an index into the **Page Table**, and a **Page offset ($\text{d}$)**, combined with the resulting frame base address to determine the final physical address.
*   Because the Page Table is stored in main memory, every instruction or data access normally requires **two memory accesses** (one for the page table, one for the item).
*   To solve this, a fast lookup hardware cache called the **Translation Look-aside Buffer (TLB)** is used to store recent page-to-frame translations.

### Virtual Memory and Thrashing
**Virtual Memory** allows processes to execute even if only part of the process is in physical memory, relying on swapping to/from a backing store. **Demand Paging** loads pages only when they are needed.

A major performance degradation issue is **Thrashing**, where the CPU spends excessive time processing **Page Faults** (when the required page is not in memory) rather than executing instructions. This occurs when memory is insufficient, causing frequently accessed pages to be constantly swapped out and immediately required again, severely increasing overhead.

### Page Replacement Policies
When a page fault occurs and no free frames are available, a page must be selected for replacement. Policies include:
*   **FIFO (First-In, First-Out):** Replaces the oldest page (the one brought in earliest).
*   **Optimal:** Replaces the page whose next use will occur **farthest in the future** (best, but impossible to implement practically).
*   **LRU (Least Recently Used):** Replaces the page that has not been used for the longest period of time.

### Segmentation
**Segmentation** divides the process into variable-sized, logically related units called segments (e.g., stack, subroutine, main program). A **Segment Table** maps the two-dimensional logical address (segment number 's' and displacement 'd') to the physical address. Each entry specifies the **Base Address** (physical starting address) and the **Limit** (segment length).

## 3.4 Cache Memory Organization

**Cache memory** is a small amount of fast memory placed between the processor and main memory. It uses a **Mapping Function** to determine where a main memory block can be stored in the cache. The three primary mapping techniques are:
1.  **Direct Mapping:** Maps a block to a single specific cache line.
2.  **Associative Mapping:** Allows a memory block to be placed in any available cache line. This is the best but most expensive method.
3.  **Set Associative Mapping:** A compromise where the cache is divided into sets, and a memory block maps only to a specific set (Block $i$ of MM maps to $\text{Set } i \bmod v$), but can be placed in any line within that set.

---

# Module 4: Concurrency Control and Deadlock

Module 4 focuses on the challenges of concurrent process execution and mechanisms to ensure mutual exclusion, specifically addressing deadlocks and synchronization problems.

## 4.1 Concurrency and Synchronization

### Cooperating Processes and Race Condition
**Cooperating processes** are those that can affect or be affected by other processes, usually through shared data. **Concurrent access** to shared data can lead to data inconsistency, a scenario called a **Race Condition**, where the outcome depends on the particular order of execution. To guard against this, only one process should manipulate the shared data at a time; hence, synchronization is required.

### Critical Section Problem
The **Critical Section (CS)** is the code segment where a process changes common variables. The **Critical Section Problem** requires a protocol ensuring that the execution of critical sections is **mutually exclusive in time** (no two processes run their CS concurrently).

Any solution must satisfy three requirements:
1.  **Mutual Exclusion:** If process $\text{P}_i$ is executing in its CS, no other process can be.
2.  **Progress:** If no process is in its CS, and some want to enter, the decision on who enters next cannot be postponed indefinitely.
3.  **Bounded Waiting:** A limit exists on the number of times other processes can enter their CS after a process requests entry.

### Solutions for Mutual Exclusion

Solutions can be implemented via software or specialized hardware:
*   **Software Solutions:** Includes algorithms like **Peterson’s Algorithm** (a correct solution satisfying all three requirements), **Strict Alternation** (using a shared `turn` variable, but failing the Progress requirement), or techniques utilizing a **Lock Variable** or **Status Flag** array.
*   **Hardware Support:** Achieved using mechanisms like **Interrupt Disabling** or special **Machine Instructions** (e.g., $\text{TestAndSet}$ or $\text{SWAP}$) that execute two or more operations atomically (uninterruptibly).

### Semaphores and Monitors
**Semaphores** are synchronization tools accessed only through two **atomic** operations: $\text{wait()}$ and $\text{signal()}$. They can be **Counting** (unrestricted integer range) or **Binary** (mutex locks, restricted to 0 or 1). Semaphores can solve the $n$-process CS problem by sharing a semaphore `mutex` initialized to 1.

A **Monitor** is a high-level abstraction containing shared data variables and procedures. It enforces synchronization by ensuring **only one process may be active within the monitor at a time**, providing inherent mutual exclusion. Monitors can be extended with **Condition Variables** ($\text{x.wait()}$ and $\text{x.signal()}$) for more complex synchronization schemes.

### Classical Synchronization Problems
These classical problems demonstrate the need for synchronization primitives like semaphores:
*   **Bounded-Buffer Problem (Producer-Consumer):** Synchronizing a producer adding items to a fixed-size buffer and a consumer removing items, ensuring the consumer waits if the buffer is empty and the producer waits if the buffer is full.
*   **Readers-Writers Problem:** Managing concurrent access to a shared data object (file) where multiple readers can access it simultaneously, but writers require exclusive access.
*   **Dining-Philosophers Problem:** A classic example of allocating multiple resources (chopsticks) among competing processes (philosophers) in a deadlock and starvation-free manner.

## 4.2 Deadlock

A **Deadlock** occurs when two or more processes wait indefinitely for an event (typically a resource release) that can only be caused by one of the waiting processes. Multithreaded programs are particularly susceptible as they compete for shared resources.

### Deadlock Characterization
Deadlock can only occur if four necessary conditions hold simultaneously:
1.  **Mutual Exclusion:** At least one resource must be non-sharable (used by only one process at a time).
2.  **Hold and Wait:** A process holding at least one resource is waiting to acquire additional resources held by other processes.
3.  **No Preemption:** Resources cannot be forcibly taken away; they must be voluntarily released by the process holding them after task completion.
4.  **Circular Wait:** A circular chain of waiting processes exists, where $\text{P}_0$ waits for a resource held by $\text{P}_1$, $\text{P}_1$ waits for $\text{P}_2$, and so on, until $\text{P}_n$ waits for $\text{P}_0$.

### Resource-Allocation Graph (RAG)
The **RAG** uses a directed graph to model resource states. If the graph contains no cycles, there is no deadlock. If a cycle exists:
*   If there is only **one instance** per resource type, a cycle is a necessary and sufficient condition for deadlock.
*   If there are **several instances** per resource type, a cycle is necessary but not sufficient; deadlock is only possible.

### Methods for Handling Deadlocks
Systems deal with deadlocks in three ways:
1.  **Deadlock Prevention:** Ensuring at least one of the four necessary conditions cannot hold.
2.  **Deadlock Avoidance:** Requiring the OS to have prior information about process resource demands to dynamically ensure the system never enters an **unsafe state** (a state where deadlock is possible).
3.  **Deadlock Detection and Recovery:** Allowing deadlock to occur and then finding and breaking the cycle.
4.  **Ignoring the problem:** Used by many OS like UNIX and Windows, pretending deadlocks never occur.

#### Deadlock Prevention Strategies
To deny the necessary conditions:
*   **Deny Hold and Wait:** Require a process to request all its resources before starting, or only when it holds zero resources. Disadvantages include low resource utilization and possible starvation.
*   **Deny No Preemption:** If a process holding resources requests a new unavailable resource, all held resources are preempted/released (implicit release).
*   **Deny Circular Wait:** Impose a total ordering on all resource types and require processes to request resources in increasing order of enumeration.

#### Deadlock Avoidance Algorithms
*   **Single instance per resource type:** Use the RAG scheme with a **claim edge** (dashed line $\text{P}_i \to \text{R}_j$) indicating a potential future request. A request is granted only if granting it does not create a cycle (thus avoiding the unsafe state).
*   **Multiple instances per resource type:** Use the **Banker’s Algorithm**. This algorithm requires each process to declare its **maximum resource need** a priori. The core idea is the **Safety Algorithm**, which attempts to find a **safe sequence** ($\text{P}_1, \text{P}_2, \ldots, \text{P}_n$) of all processes such that the resource needs of each $\text{P}_i$ can be met by available resources plus resources held by all preceding processes ($\text{P}_j, j<i$).

#### Deadlock Detection and Recovery
For systems without prevention or avoidance, a detection algorithm is required.
*   If resources are **single-instance**, a **Wait-For Graph (WFG)** is maintained (obtained by collapsing resource nodes from the RAG). A cycle in the WFG indicates deadlock.
*   If resources are **multiple-instance**, a more complex algorithm similar to the Banker's Safety Algorithm is used, involving matrices for Available, Allocation, and Request vectors, searching for a sequence where all processes can finish.

**Recovery** involves breaking the deadlock by either:
1.  **Process Termination:** Aborting all deadlocked processes, or aborting one at a time until the cycle is broken (often based on factors like process priority or resources consumed/needed).
2.  **Resource Preemption:** Successively taking resources from a victim process, requiring the victim process to **Rollback** to a safe state (or be totally aborted and restarted). Starvation must be prevented by ensuring a process is not repeatedly selected as a victim.

---

# Module 5: File and I/O Management

Module 5 covers methods for accessing data stored on disks and the foundational techniques the operating system uses to manage communication with hardware peripherals.

## 5.1 File Access Methods

Files, which are data objects managed by the OS, can be accessed in three primary ways:
1.  **Sequential Access:** Data is accessed in linear order, one record after the next. A pointer moves sequentially through the file (e.g., text files, audio files).
2.  **Direct Access:** The file is viewed as a numbered sequence of blocks or records, allowing reading or writing to occur in any arbitrary order. This is crucial for retrieving filtered information quickly, such as in database systems.
3.  **Index Sequential Method:** This uses an **index** structure containing pointers to various data blocks within the file. This allows the user to quickly search the index first and then directly access the required block of data.

## 5.2 I/O Organization

### I/O Device Categories
External I/O devices are typically grouped into three categories:
1.  **Human readable:** Devices for communication with the user (e.g., keyboard, display, printer).
2.  **Machine readable:** Devices for communication with electronic equipment (e.g., disk drives, sensors).
3.  **Communication:** Devices for communicating with remote devices (e.g., modems, NICs).

Devices also differ widely in characteristics like data rate, complexity of control, unit of transfer (blocks or streams), data representation, and error conditions. Block-oriented devices (like hard disks) store and transfer data in fixed-size blocks, while stream-oriented devices (like printers or mice) transfer data as a flow of bytes.

### Techniques for Performing I/O
Three fundamental techniques exist for performing I/O transfers:

1.  **Programmed I/O:** The CPU must repeatedly check (or "poll") the I/O interface's status flag to see if the device is ready for data transfer. This is time-consuming as it keeps the processor needlessly busy in a program loop.
2.  **Interrupt-Driven I/O:** The processor issues an I/O command and continues executing instructions. The I/O device sends an **interrupt signal** when the operation is complete. If the requesting process must wait, the OS puts it into a blocked state.
3.  **Direct Memory Access (DMA):** A **DMA module** controls the direct exchange of data between main memory and an I/O module, thereby relieving the CPU from the burden of managing the transfer itself.

### I/O Buffering
A **buffer** is a memory area used to temporarily store data being transferred between devices, particularly useful when there is a **speed mismatch** between the data producer and consumer. Types of buffering include Single, Double, and Circular I/O Buffering.

## 5.3 Disk Scheduling

Disk scheduling algorithms aim to minimize the time spent positioning the read/write heads. **Access time** is the sum of **seek time** (time to move the head to the correct track) and **rotational delay** (time for the correct sector to spin under the head).

Disk scheduling algorithms optimize the order of servicing track requests:

*   **First-In, First-Out (FIFO):** Services requests in the sequential order they arrive. While fair, its performance can approximate random scheduling if there are many competing processes.
*   **Shortest Service Time First (SSTF):** Always selects the request that requires the **least movement of the disk arm** from its current position. This minimizes seek time but can potentially lead to starvation for requests far from the current head position.
*   **SCAN (Elevator Algorithm):** The arm moves continuously in one direction, servicing all requests in its path until it reaches the end of the disk (or the last request in that direction—known as **LOOK**). It then reverses direction and repeats.
*   **C-SCAN (Circular SCAN):** Restricts the scan to **one direction only**. When the arm reaches the end of the disk, it immediately returns to the opposite end without servicing any requests on the return sweep.
*   **LOOK and C-LOOK:** These are variations of SCAN and C-SCAN, respectively, where the arm reverses direction only when it reaches the **last request** in that direction, preventing unnecessary traversal to the absolute end of the disk.

### RAID
**RAID (Redundant Array of Independent Disks)** uses a set of disk storage units organized as a single logical unit. Data is distributed across the drives, and **redundant capacity** is employed (via parity) to allow for data repair, improving dependability.

---

# Module 6: Advanced Computer Architecture

Module 6 explores parallel systems, processor classification, multicore design, specialized hardware like GPUs, and the topologies used to interconnect these systems.

## 6.1 Parallel Architectures and Flynn's Taxonomy

### Characteristics of Parallel Systems
Parallel processing systems aim to improve processing speed by dividing a program into multiple parts that execute concurrently. These are often called multiprocessors or multicomputers.

### Flynn’s Taxonomy
**Flynn’s taxonomy** classifies parallel computer architectures based on two orthogonal criteria: the number of concurrent **instruction streams** and **data streams**.

The four categories are:

1.  **SISD (Single Instruction, Single Data):** A conventional uniprocessor executing a single instruction stream on a single data stream (e.g., standard von Neumann architecture).
2.  **SIMD (Single Instruction, Multiple Data):** A single control unit executes the **same instruction** across multiple processing units (PUs) simultaneously on **different data streams**. This architecture is highly suited for **data level parallelism**. **Processor arrays** fall into this category.
3.  **MISD (Multiple Instruction, Single Data):** Multiple functional units execute **different instructions** on the **same data set**. This architecture is rare but used primarily in fault-tolerant systems for redundant execution.
4.  **MIMD (Multiple Instruction, Multiple Data):** The most common architecture, where each processor executes **different instruction streams** asynchronously on **different data units**. Multiprocessors and multicomputers fall into this category.

## 6.2 Multiprocessors and Multicore Systems

Parallel systems can be characterized by how tightly processors are **coupled**:
*   **Tightly Coupled Systems (Multiprocessors):** Contain multiple CPUs connected at the bus level, sharing a central memory and featuring fast intercommunication. They often run a single instance of the operating system.
*   **Loosely Coupled Systems (Multicomputers/Distributed Systems):** Consist of processors with distributed memory; each processor has its own memory and communicates via message passing or interconnection switching, sometimes running different operating systems.

Multiprocessors are divided by memory access characteristics:

1.  **Uniform Memory Access (UMA) / Symmetric Multiprocessor (SMP):** All processors share physical memory and access all memory words with **equal access time**. Multicore processors are small UMA systems where the first shared cache acts as the communication channel. In UMA systems, the hardware must address the **cache coherence problem** because separate caches may hold conflicting copies of the same memory block.
2.  **Non-Uniform Memory Access (NUMA):** Shared memory is **physically distributed** among processors (local memories), leading to **variable access time** (accessing local memory is quicker than remote memory). Programs written for UMA systems can run on NUMA systems, though with varied performance. To maintain cache consistency, NUMA systems use protocols like the **directory-based protocol** (in CC-NUMA systems).

**Hardware Multithreading** enables multiple threads to be processed simultaneously to tolerate memory operation latency and improve system throughput. Types include:
*   **Fine Grained Multithreading:** Switches among threads almost every cycle to keep the pipeline utilized, effectively tolerating control and data dependency latencies.
*   **Coarse Grained Multithreading:** Switches threads only when the current thread encounters a major stall (e.g., cache miss or synchronization event).
*   **Simultaneous Multithreading (SMT):** The most advanced type, which issues instructions from multiple threads concurrently to the execution units of a wide superscalar processor, filling unused instruction slots to maximize utilization.

## 6.3 Specialized Architectures and Network Topologies

### Graphics Processing Units (GPUs)
A **GPU** is a single-chip processor specialized for managing and boosting the performance of video and graphics. It is a dedicated parallel processor featuring **thousands of cores** for highly parallel operations, contrasting sharply with a CPU’s fewer cores and shallower pipeline.

The GPU pipeline stages include:
*   **Input Assembler:** The bridge that pulls geometry information from the CPU/system memory.
*   **Vertex Processing:** Performs operations like transformation, skinning, and lighting on input vertices.
*   **Pixel Processing:** Computes the final color for pixels, including texture mapping.

### Clusters and Warehouse Scale Computers (WSCs)
A **Cluster** is a collection of networked computers acting as one larger system. A **Warehouse Scale Computer (WSC)** is a massive cluster (tens of thousands of servers) that forms the foundation of internet services. WSCs prioritize massive scalability, energy efficiency, and **dependability via redundancy**. Due to the independent nature of user requests, WSCs primarily exploit **Request-Level Parallelism (RLP)**.

### Multiprocessor Network Topologies
**Network Topology** refers to the way nodes (processors/memories/switches) are interconnected, significantly affecting system cost, scalability, and performance. Topologies are classified by two groups:

**A. Cube Based Networks** (known for symmetry, scalability, and rich interconnection):
*   **Binary Hypercube (n-cube):** An $n$-dimensional cube with $2^n$ nodes and $n$ edges per node. It has a logarithmic diameter ($n$) and high bisection width ($2^{n-1}$), making it attractive, but its node degree ($n$) increases with network size, making it difficult to scale well.
*   **Folded Hypercube (FHC):** A variation achieved by adding extra links, resulting in a halved diameter and better average distance.
*   **Crossed Cube (CC):** Has the same complexity as a hypercube but its diameter is almost half of its corresponding hypercube.

**B. Linearly Extensible Networks** (generally simpler, avoiding exponential expansion):
*   **Linear Array (LA):** A 1D network where internal nodes have a degree of 2. Its diameter ($n-1$) increases linearly with the number of nodes, making it unsuitable for large systems.
*   **Binary Tree (BT):** Has a low, constant node degree (3) regardless of size. Its diameter is low (logarithmic function of $n$), but its **bisection width is very poor** (only 1).
*   **Mesh Network (2D/q-dimensional):** Nodes arranged in a lattice. A 2D mesh has a constant node degree (4). It has a high bisection width (e.g., $\sqrt{n}$ for 2D mesh with $n$ nodes), which is good for parallelism.
*   **Torus (Toroidal Mesh):** An extension of the mesh where exterior nodes are connected (wrap-around), lowering the diameter compared to a non-toroidal mesh.
*   **Ring (R):** A linear array connected end-to-end, characterized by a constant node degree ($d=2$) and a constant bisection width (2).
*   **Butterfly Network:** An indirect topology arranged in ranks and columns, often related to the Hypercube.
