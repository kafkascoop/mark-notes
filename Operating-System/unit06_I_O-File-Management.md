

# ⚙️ Unit 6: I/O Management and File Systems

## 🔌 Topic 1: I/O Hardware and Principles of I/O Software

### **Introduction: The Gateway to the World** 🌍

The Input/Output (I/O) subsystem is the link between the computer and the external world (users and storage devices). The OS's job is to manage this complexity, ensuring efficient and error-free data transfer.

### **I/O Hardware: The Physical Components** 🛠️

* **I/O Devices:** The physical hardware that performs input or output (e.g., keyboard, mouse, printer, disk drive, network card).
* **Device Controller (Adapter):** A circuit board or chip that operates a port, bus, or device. It's the **local CPU** for the device.
    * It contains control registers, a data buffer, and error-correcting code logic.
    * It presents a **clean, standard interface** to the OS's device driver, hiding the messy details of the device itself.
* **I/O Port:** A collection of specialized CPU instructions (like `IN` and `OUT`) or memory-mapped locations used to communicate with the device controller's registers.

### **Direct Memory Access (DMA)** 🚀

* **Problem without DMA:** For large data transfers (like reading a file from disk), the CPU has to constantly interrupt its work to move data word-by-word between the device controller's buffer and main memory. This wastes CPU time.
* **DMA Concept:** DMA allows the device controller to transfer an entire block of data directly to or from main memory **without intervention from the CPU**.
* **How it Works:** The CPU tells the **DMA controller** (a specialized chip) the address, count, and direction of the transfer. The DMA controller handles the bus arbitration and data transfer. The CPU is only interrupted **once** when the entire transfer is complete.

### **Principles of I/O Software** 💻

I/O software is often structured in layers to keep the core OS (kernel) clean and manage complexity.

* **Goal of Interrupt Handlers:** When an I/O operation finishes, the device controller generates an **interrupt**. The **Interrupt Handler** is the first piece of OS code to run.
    * Its goal is to quickly and efficiently service the interrupt, clear the device, and unblock the waiting process. It must be as fast as possible to minimize disruption.
* **Device Drivers (The Translators):** The software layer dedicated to managing one specific type of I/O device.
    * It is the **only code that knows the intricate details** of the controller.
    * It takes abstract requests from the OS (e.g., "Read block 10") and translates them into a sequence of low-level commands for the controller's registers.
* **Device-Independent I/O Software:** A uniform interface layer above the device drivers.
    * **Goals:** Provide a standard function set for all devices (e.g., `open`, `read`, `write`) and perform general functions like buffering, blocking/unblocking processes, and error reporting.

---

## 💿 Topic 2: Secondary Storage Structure and Disk Management

### **Disk Structure (The Physical Layout)** 📊

A typical magnetic disk structure:
* **Platters:** Circular metal plates coated with magnetic material.
* **Tracks:** Concentric rings on the platter surface where data is recorded.
* **Sectors:** Angular segments of a track; the smallest unit of transfer.
* **Cylinders:** A set of tracks that are at the same radial position on all platters. Reading data in the same cylinder is fast, as the read/write heads don't need to move.

### **Disk Management Basics** 🛠️

* **Disk Formatting (Low-Level):** Dividing the disk into sectors that the disk controller can read and write. This involves filling the disk with special control structures (headers, data, trailers).
* **Boot Block:** A small area on the disk (usually the first sector) that holds the initial bootstrap program needed to load the full operating system kernel into memory when the computer starts.
* **Bad Blocks:** Sectors that have been physically damaged. The OS (or controller) must manage these by marking them unusable or by swapping them out for spare sectors.

### **Disk Scheduling Algorithms** 🔄

The movement of the read/write head (the **seek time**) is the biggest bottleneck in disk I/O. **Disk Scheduling** algorithms aim to minimize seek time by optimizing the order of disk requests.

* **FCFS (First-Come, First-Served):** Processes requests in the order they arrive.
    * **Pro:** Simple and fair.
    * **Con:** Very inefficient, especially with many requests scattered across the disk.
* **SSTF (Shortest Seek Time First):** Services the request that is **closest** to the current head position.
    * **Pro:** High throughput, much faster than FCFS.
    * **Con:** Can cause **starvation** for requests far from the current head position.
* **SCAN (Elevator Algorithm):** The head moves from one end of the disk to the other, servicing all requests in its path. When it reaches the end, it reverses direction.
    * **Pro:** Prevents starvation and provides a predictable, low variance in response time.
* **C-SCAN (Circular SCAN):** The head services requests only while moving in one direction (e.g., inward). When it reaches the end, it immediately returns to the starting end **without servicing any requests** on the return trip.
    * **Pro:** More uniform wait time than SCAN, as it gives more fair access to the tracks at the outer edge.

---

## 📂 Topic 3: File Management and Directory Structure

### **Concept of File and File Operations** 📝

* **File Definition:** A file is a **logical storage unit** defined by its creator. It is the smallest unit of output that can be named and manipulated independently. It is essentially an abstract data type.
* **File Attributes:** Information stored by the OS about a file (name, type, location, size, time/date of creation, protection/permissions).
* **Common File Operations:** The basic system calls provided by the OS to manipulate files:
    * `Create()` (Allocate space and entry in directory).
    * `Write()` (Write data, advancing the write pointer).
    * `Read()` (Read data, advancing the read pointer).
    * `Reposition/Seek()` (Move the current file pointer to a specific location).
    * `Delete()` (Remove file and free its space).
    * `Truncate()` (Erase contents, but keep file attributes).

### **Access Methods** 🔑

How processes access data within a file:
1.  **Sequential Access:** Data is processed in order, one record after another. (Like reading a tape drive or streaming data). Most common.
2.  **Direct (Relative) Access:** Records are accessed rapidly and randomly. The file is viewed as a numbered sequence of blocks. (Useful for database systems where rapid lookup is needed).

### **Directory Structure** 🌳

* **Directory:** A collection of nodes containing information about all files and subdirectories.
* **Goal:** Organize the files to allow users to efficiently locate and use them.
* **Structure Types:**
    * **Single-Level Directory:** All files are in one directory. Simple but prone to naming conflicts.
    * **Two-Level Directory:** Each user has their own directory. Solves naming conflicts but makes sharing difficult.
    * **Tree-Structured Directory (Most Common):** A hierarchical structure where every file/directory has a unique path from the root. Supports grouping and sharing.

### **Directory Implementation** 🛠️

How the OS stores the directory on disk:
* **Linear List:** The simplest method. The directory is a linear list of file names and pointers to data blocks.
    * **Pro:** Easy to implement.
    * **Con:** Slow to search, especially for large directories.
* **Hash Table:** A hash function is used to convert the file name into an index in a hash table.
    * **Pro:** Very fast searching and insertion (on average).
    * **Con:** Collisions (multiple names hash to the same location) must be handled, and size is fixed.

---

## 📦 Topic 4: File System Structure and Allocation Methods

### **File System Structure** 💾

A layered view of the File System:
1.  **Application Programs:** The user's interaction point (e.g., text editor, compiler).
2.  **Logical File System:** Manages metadata, directories, and protection/security. Contains the File Control Blocks (FCBs).
3.  **File Organization Module:** Translates logical block addresses (LBN) into physical block addresses (PBN). Manages free space.
4.  **Basic File System:** Issues generic commands to the device drivers.
5.  **I/O Control:** Contains device drivers and interrupt handlers (Topic 1).

### **Allocation Methods (How File Data is Stored)** 🧱

These methods determine how the disk space is allocated to store file blocks.

| Method | Concept | Pros | Cons |
| :--- | :--- | :--- | :--- |
| **Contiguous** | Each file occupies a **single, contiguous set of blocks** on the disk. | **Excellent performance** (fast sequential and direct access). Simple to implement. | **External Fragmentation** (major problem). File size must be known in advance. |
| **Linked** | Each file is a **linked list of disk blocks**. Each block contains a pointer to the next block. | **No external fragmentation.** Easy file growth. | **Slow direct access** (must traverse the list). Pointers consume space. |
| **Indexed** | A dedicated **index block** stores pointers to all the data blocks of the file. | **Fast direct access** (just read the index block). No external fragmentation. | **Overhead** for the index block itself. Managing large files requires complex multi-level indexing. |

### **Free-Space Management** 📝

How the OS keeps track of which disk blocks are free (unallocated).

1.  **Bit Vector (Bit Map):** A vector where each bit corresponds to a disk block. If the bit is 1, the block is free; if 0, the block is allocated.
    * **Pro:** Simple and efficient for finding the first free block.
    * **Con:** The entire bit vector must be stored in memory for a large disk (memory overhead).
2.  **Linked List:** The free blocks themselves form a linked list. Each free block stores a pointer to the next free block.
    * **Pro:** No space overhead for a separate map.
    * **Con:** Slow to traverse to find a contiguous block.
3.  **Grouping:** Stores the addresses of $N$ free blocks in the **first free block**. The last address points to the next block containing $N$ more addresses. (A hybrid approach).

### **Efficiency and Performance** ⚡

* **Efficiency:** How the resource is used (e.g., minimizing disk space wasted by allocation methods).
* **Performance:** The speed of file access.
* **Key factors influencing performance:**
    * **Disk Cache (Buffer Cache):** A fast, small memory area in RAM that stores frequently used disk blocks.
    * **Block Size:** Larger blocks reduce the number of I/O operations but increase internal fragmentation.
    * **Disk Scheduling:** Choosing an effective algorithm (like C-SCAN) significantly improves performance by reducing seek time.
    * **Locality of Reference:** Organizing files so that related blocks are physically close together improves access speed.