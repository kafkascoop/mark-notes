

# 🚀 Unit 2: Processes and Process Scheduling

## 💡 Topic 1: Processes (The Program in Action)

### **Introduction: The Birth of a Process** 👶

A **program** is a passive entity—it's just a file of instructions stored on your disk, like a recipe book. A **process** is the program's recipe being actively cooked! It is an **active entity** that needs resources (CPU time, memory, I/O) to complete its task.

### **Core Concepts and Definitions** 📖

#### **Definition and Components**
* **Process Definition:** A process is a **program in execution**. It is the basic unit of work in a modern time-sharing OS.
* **Key Components of a Process:**
    * **Program Counter (PC):** Points to the next instruction to be executed.
    * **Stack:** Contains temporary data (function parameters, return addresses, local variables).
    * **Data Section:** Contains global variables.
    * **Text Section:** Contains the program code (instructions).

#### **Process Relationship (Family Tree)**
* Processes can create other processes, leading to a **Parent-Child** relationship, often forming a **process tree** structure.
* **Mechanism (UNIX Style):** A parent uses the `fork()` system call to create a child process. The child is initially an *exact copy* of the parent. The child then uses the `exec()` system call to load a new program to run.

### **Process States and Transitions** 🚦

A process moves through various stages during its lifetime. The OS kernel is responsible for managing these transitions.

#### **The 5-State Model**
1.  **New:** The process is being created. (It hasn't been loaded into main memory yet.)
2.  **Ready:** The process is loaded into main memory and is **waiting** for the CPU to be assigned to it.
3.  **Running:** Instructions are being executed by the CPU.
4.  **Waiting/Blocked:** The process is waiting for some event to occur, such as an I/O completion or a signal. (It cannot proceed even if the CPU is free).
5.  **Terminated:** The process has finished execution and is waiting to be removed from memory.



#### **Key Transitions**
* **Ready → Running:** **Dispatch** (The CPU Scheduler picks it).
* **Running → Ready:** **Interrupt** (A hardware interruption or a time slice ends, forcing preemption).
* **Running → Waiting:** **I/O Request/Wait** (The process needs to wait for a file read or user input).
* **Waiting → Ready:** **I/O Completion/Signal** (The event it was waiting for has occurred).

### **Process Control Block (PCB)** 🆔

* **Concept:** The **PCB** (sometimes called the Task Control Block) is the **metadata** or **passport** of the process. It's a data structure in the kernel space that stores all the information the OS needs to manage a specific process.
* **Story:** When a process is not running, its entire existence is stored in its PCB.

| Key Fields in the PCB | Purpose |
| :--- | :--- |
| **Process State** | New, Ready, Running, Waiting, Terminated. |
| **Program Counter** | Address of the next instruction to execute. |
| **CPU Registers** | Content of all CPU registers when the process was interrupted. |
| **CPU Scheduling Information** | Process priority, pointers to scheduling queues. |
| **Memory Management Information** | Base and limit registers, page tables. |
| **I/O Status Information** | List of allocated I/O devices, open files. |

### **Context Switching** 🔄

* **Definition:** The mechanism of the OS saving the **state** (the PCB content) of the currently running process and loading the **state** of the next process to be run.
* **Analogy:** A student (CPU) working on one textbook (Process A). When the bell rings (Interrupt), the student carefully **closes the book and bookmarks the page** (saves PCB A), then **opens another textbook to the correct page** (loads PCB B) and starts working on it.
* **Overhead:** Context switching is pure **overhead** because the system is doing useful work. The time it takes is non-productive and should be minimized.

### **Tips to Memorize** ✨

* **PCB Mnemonic:** Remember the six main categories: **S**tate, **P**C, **R**egisters, **S**cheduling, **M**emory, **I**/O.

---

## 🧵 Topic 2: Threads (The Lightweight Process)

### **Introduction: Sharing the Kitchen** 👨‍🍳

A process is like a large restaurant (with its own kitchen, staff, menu, and cash register). A **thread** is like a single waiter or chef working within that same restaurant. Multiple threads within one process can work **concurrently** to complete tasks.

### **Core Concepts and Definitions** 📚

* **Thread Definition:** A thread is a **lightweight process (LWP)** or a **basic unit of CPU utilization**. It represents a single sequence of execution within a process.
* **Shared Resources (Within a Process):** Multiple threads within the same process share the following:
    * Text Section (Code)
    * Data Section (Global variables)
    * Operating System Resources (Open files, signals).
* **Private Resources (Per Thread):** Each thread has its own unique:
    * Thread ID
    * Program Counter (PC)
    * Register Set
    * Stack (for local variables and function calls)

### **Benefits of Threads (The Four S's)** ✅

1.  **Responsiveness:** If one thread blocks (e.g., waiting for I/O), the entire program doesn't stop. Other threads can continue running, keeping the application responsive.
2.  **Resource Sharing:** Threads share the memory and resources of their parent process. This is more efficient than creating separate processes.
3.  **Economy (Cost):** **Creating a thread is much cheaper and faster** than creating a new process. Thread context switching also takes less time.
4.  **Scalability:** Allows a single process to use multiple CPU cores (**Multicore Programming**) simultaneously, significantly boosting performance.

### **Types of Threads** 📊

#### **1. User-Level Threads (ULT)**
* **Management:** Managed entirely by a **thread library** in user space. The OS kernel is unaware of their existence.
* **Analogy:** You manage your own workload without telling the school principal (OS).
* **Con:** If one ULT thread performs a blocking system call, the entire process (and all its threads) is blocked.
* **Pro:** Very fast to create and switch between, as no kernel intervention is needed.

#### **2. Kernel-Level Threads (KLT)**
* **Management:** Managed and scheduled directly by the **OS kernel**.
* **Analogy:** The school principal (OS) knows and manages every teacher (thread).
* **Pro:** If one KLT thread blocks, the kernel can simply schedule another thread from the same process, preventing the entire process from blocking.
* **Con:** Slower to create and manage than ULTs due to the overhead of kernel involvement.
* **Examples:** Windows, Linux, macOS.

### **Concept of Multithreading** 🌐

* **Definition:** The ability of an OS to support multiple, concurrent threads of execution *within a single process*.
* **The Power of Mapping:** The OS needs a way to map user-level threads to kernel-level threads.
    * **Many-to-One:** Many ULTs map to a single KLT. (Blocks the whole process).
    * **One-to-One:** Each ULT maps to a separate KLT. (Best for parallelism on multi-core CPUs).
    * **Many-to-Many:** Many ULTs map to a smaller or equal number of KLTs. (Flexible, balanced approach).

### **Common Mistakes to Avoid** ❌

* **Thread vs. Process:** Don't confuse them! A process owns resources; a thread **consumes** resources within a process.
* **Blocking:** Remember the key difference: a blocking system call by a **ULT** blocks the whole process; a blocking call by a **KLT** only blocks that specific thread.

---

## ⚙️ Topic 3: Process Scheduling

### **Introduction: The Traffic Controller** 🚥

The CPU is the most valuable resource. **Process Scheduling** is the act of selecting a process from the Ready Queue and allocating the CPU to it. The goal is to maximize efficiency and minimize user wait time.

### **Foundation and Scheduling Objectives** 🎯

* **Foundation (When does scheduling happen?):**
    * When a process switches from **Running → Waiting** (Non-preemptive).
    * When a process switches from **Running → Ready** (Preemptive, e.g., time slice ends).
    * When a process switches from **Waiting → Ready**.
    * When a process **Terminates**.
* **Objectives (What makes a good scheduler?):**
    1.  **Fairness:** Every process must get its fair share of the CPU.
    2.  **Efficiency/Utilization:** Keep the CPU as busy as possible (ideally 40%–90%).
    3.  **Throughput:** Maximize the number of processes completed per unit of time.
    4.  **Response Time:** Minimize the time from submission to the first response (crucial for interactive systems).
    5.  **Turnaround Time:** Minimize the total time from submission to completion (waiting + running).
    6.  **Waiting Time:** Minimize the total time spent in the Ready Queue.

### **Types of Schedulers** 👨‍💼

| Scheduler | Frequency | Role | Analogy |
| :--- | :--- | :--- | :--- |
| **Long-Term (Job Scheduler)** | Infrequent (seconds/minutes) | Selects which processes are loaded from **disk** (spool) into **main memory** (Ready Queue). | **Bouncer at a club**—Controls who gets inside (the degree of multiprogramming). |
| **Short-Term (CPU Scheduler)**| Very Frequent (milliseconds) | Selects which process in the **Ready Queue** gets the **CPU**. | **Traffic Cop**—Directly manages the flow of traffic (processes). |
| **Medium-Term Scheduler** | Medium (seconds) | Handles **swapping**—removes a process from memory to disk (suspended state) to reduce the degree of multiprogramming. | **Theater usher**—Moves processes in and out of the main seating area (memory). |

### **Scheduling Criteria: The Metrics** 📏

| Criteria | Definition | Goal | Exam Focus |
| :--- | :--- | :--- | :--- |
| **CPU Utilization** | Percentage of time the CPU is busy. | Maximize (keep it busy). | Performance Metric. |
| **Throughput** | Number of processes completed per unit time. | Maximize (more output). | Performance Metric. |
| **Turnaround Time (TT)** | $\text{Completion Time} - \text{Arrival Time}$ | Minimize (finish faster). | Calculation Metric. |
| **Waiting Time (WT)** | $\text{TT} - \text{Burst Time (Execution)}$ | Minimize (less idle time). | Calculation Metric. |
| **Response Time (RT)** | $\text{Time of First Response} - \text{Arrival Time}$ | Minimize (crucial for interactive systems). | User Experience Metric. |

---

## 📏 Topic 4: Scheduling Algorithms (The Rules)

### **A. Pre-emptive vs. Non-pre-emptive** 🥊

This is the most critical distinction in scheduling algorithms:

* **Non-pre-emptive:** Once the CPU is allocated to a process, it holds the CPU until it terminates or requests I/O (moves to Waiting state). **The CPU cannot be forcibly taken away.**
* **Pre-emptive:** A process can be **interrupted** and forced to yield the CPU to another process, usually after a time slice expires or a higher priority process arrives.

### **B. Major Scheduling Algorithms** ⚙️

#### **1. FCFS (First-Come, First-Served)**
* **Type:** **Non-pre-emptive.**
* **Concept:** Processes are executed in the order they arrive in the Ready Queue. Simple queue (FIFO).
* **Analogy:** Waiting in a line for a ticket counter.
* **Pros:** Simple to implement.
* **Cons:** Poor performance. Suffers from the **Convoy Effect**, where a small process must wait for a single very large process to finish, leading to high average waiting time.

#### **2. SJF (Shortest Job First)**
* **Concept:** The CPU is allocated to the process that has the **smallest next CPU burst time**.
* **Optimality:** SJF is **provably optimal** in minimizing the **average waiting time** for a given set of processes.
* **Problem:** It is **impossible to know the length of the next CPU burst** in advance (a key flaw). OS often uses prediction/estimation based on past bursts.
* **Types:**
    * **Non-pre-emptive SJF:** When the CPU is free, the next shortest job is selected.
    * **Pre-emptive SJF (SRTF - Shortest Remaining Time First):** If a new process arrives whose required CPU time is less than the **remaining time** of the currently executing process, the current process is preempted.

#### **3. RR (Round Robin)**
* **Type:** **Pre-emptive.** Designed specifically for time-sharing and interactive systems.
* **Concept:** Processes are executed in a cyclical manner. A small unit of time, called a **time quantum** ($\Delta t$), is defined. Each process gets the CPU for at most one quantum.
* **Analogy:** Taking turns at a board game.
* **Pros:** Good **Response Time** (RT) because every process gets a little CPU time quickly. Fair distribution of resources.
* **Cons:** Performance heavily depends on the quantum size.
    * **Large Quantum:** RR becomes like FCFS.
    * **Small Quantum:** Causes too many **Context Switches** (high overhead).

### **Tips to Memorize** 🧠

* **SJF Optimality:** Remember **SJF minimizes average Waiting Time**. This is a common exam question.
* **RR Key:** Always think of the **Time Quantum**. If a process finishes before its quantum, it voluntarily releases the CPU.

---

## 🌐 Topic 5: Advanced Scheduling

### **A. Multiprocessor Scheduling** ⚙️

When you have multiple CPU cores, scheduling gets more complex.

* **The Challenge:** **Load Sharing**—how to distribute the workload fairly among all available CPUs.
* **Types of Multiprocessor Scheduling:**
    1.  **Asymmetric Multiprocessing (AMP):** One processor (the **master server**) handles all scheduling decisions, I/O processing, and system activities. Other processors only execute user code. **Simple but single point of failure.**
    2.  **Symmetric Multiprocessing (SMP):** Each processor is **self-scheduling**. They all have their own scheduler and examine the common Ready Queue (or their private Ready Queue) to select a process to run. **Most common approach today.**
* **Processor Affinity:** Most SMP systems try to keep a process running on the same CPU core it ran on last time (**soft affinity**) to take advantage of the data remaining in the CPU's cache.

### **B. Real-Time Scheduling** ⏱️

This is used in systems where correctness depends not just on the result but also on **when** the result is produced (e.g., flight control, pacemaker).

* **Hard Real-Time:** Missing a deadline is a **total system failure** (e.g., stopping a train).
* **Soft Real-Time:** Missing a deadline is undesirable but tolerable (e.g., missing a frame in a video stream).

#### **1. RM (Rate Monotonic Scheduling)**
* **Type:** **Static Priority**, Pre-emptive.
* **Concept:** Priority is assigned based on the **period** (rate) of the task. The shorter the period (i.e., the higher the rate/frequency), the higher the priority.
* **Simplicity:** Priorities are fixed at the start and never change.

#### **2. EDF (Earliest Deadline First)**
* **Type:** **Dynamic Priority**, Pre-emptive.
* **Concept:** Priority is assigned based on the **absolute deadline**. The process whose next deadline is the **earliest** receives the highest priority.
* **Optimality:** EDF is considered **optimal** because it can theoretically schedule any set of tasks as long as their total CPU utilization is $\le 100\%$.
* **Complexity:** More complex to implement because priorities must be recalculated dynamically as deadlines approach.

### **Important Keywords** 📌

* **Pre-emption:** Forcibly taking the CPU away.
* **Dispatch Latency:** The time it takes for the scheduler to stop one process and start running another.
* **Utilization Bound:** The maximum CPU percentage that can be used while still guaranteeing all tasks meet their deadlines (used in Real-Time Systems).

### **Summary or Revision Points** 💡

* A **Process** is a program in execution, defined by its **PCB**.
* A **Thread** is a single execution path within a process, sharing the process's code and data.
* **Context Switching** is the non-productive overhead of saving/loading PCBs.
* The **Short-Term Scheduler** (CPU Scheduler) uses criteria like **WT** and **TT** to choose the next process.
* **RR** is best for responsiveness; **SJF** is best for minimizing average wait time.
* **RM** (fixed priority) and **EDF** (dynamic priority) are the key Real-Time algorithms.