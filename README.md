# Memory Management System with Paging and Swap Memory

## Overview

This project implements a memory management system that handles paging and swap memory for processes running on a simulated operating system. The system operates using a paging mechanism to manage main memory and swap memory, along with a page replacement strategy using FIFO (First In, First Out) and LRU (Least Recently Used). The primary goal is to ensure that memory is allocated to processes efficiently, and when memory is full, swapping occurs to maintain functionality.

This project is part of **Assignment 3** for the CS3500 - Operating Systems course and provides a hands-on experience with memory management techniques such as paging and swapping. The assignment simulates a system where user-specified executables run, accessing and modifying memory using basic arithmetic commands (e.g., `add`, `sub`, `print`, `load`). If a page of memory is not currently in the main memory, the system will move pages between main memory and swap memory as necessary.

## Features

- **Paging System:** Handles memory allocation in fixed-size pages for both main and swap memory.
- **FIFO Page Replacement:** When main memory is full, it evicts the oldest page and loads the required page into memory.
- **LRU Page Replacement:** When main memory is full, it evicts the Least Recently Used page and loads the required page into memory.
- **Memory Operations:** Supports loading of executables and operations such as `add`, `sub`, `load`, and `print` on memory addresses.
- **Process Management:** Allows loading and running multiple processes, each with its own page table and process ID.
- **Command Interpreter:** Reads commands from an input file to manage memory and process operations interactively.

## Input Format

The input consists of several parameters that define the memory configuration, as well as executable files containing instructions for the processes:

1. **Main memory size (M)**: Specifies the size of the main memory in kilobytes.
2. **Swap memory size (V)**: Specifies the size of the swap memory in kilobytes.
3. **Page size (P)**: Specifies the page size in bytes.
4. **Executable files**: Each executable contains: - The assigned size (in KB) of the executable. - A set of memory-related commands (`add`, `sub`, `print`, `load`).

### Example Input:

- `M = 32 KB` - `V = 32 KB` - `P = 512 bytes`

This setup would create a main memory with 64 pages and a swap memory with 64 pages (both of size 512 bytes each).

## Commands Supported

The system supports several commands that allow interaction with processes and memory:

1. **load filename1 filename2 ...**  :- Loads the specified executables into memory. If main memory is full, the system loads the executable into swap memory. If both main and swap memory are full, it stops loading and prints an error message.

   **Output Example:** file1 is loaded and assigned process id 1
                        file3 could not be loaded - memory is full


2. **run pid** :- Executes the program identified by its process ID (pid). During execution, it may bring pages from swap memory into main memory if they are required.

3. **kill pid** :- Terminates the process identified by the given pid and frees all the memory allocated to that process.

4. **listpr** :- Lists all active process IDs in both main memory and swap memory, sorted by pid.

5. **pte pid file** :- Outputs the page table entry information of a process (identified by pid) to the specified file. This includes the logical page number, physical page number, and whether the page is present in main memory.

6. **pteall file** :- Outputs the page table entry information for all processes in ascending order of their pids to the specified file.

7. **print memloc length** :- Prints the contents of the specified range of memory addresses (from `memloc` to `memloc + length - 1`).

8. **exit** Terminates the program, cleans up all allocated memory, and exits the system.

## Paging and Swap Memory

The system simulates both **main memory** and **swap memory** using paging. Pages are fixed-sized blocks of memory. A page in main memory contains process data, and if more processes are loaded than main memory can hold, pages are swapped out to **swap memory**.

### Memory Allocation

- **Main Memory Allocation:** If there is space in the main memory, the process's pages are loaded into it. - **Swap Memory Allocation:** If main memory is full, pages are loaded into swap memory. The swap memory holds pages until they are needed. - **Page Table:** Each process has its own page table, which keeps track of the mapping between logical memory addresses and physical memory pages.

### Page Replacement

If the system requires a page that is not in main memory, it will: 1. **Check for free space in main memory.** If there is space, the page will be loaded into memory. 
2. **Use FIFO or LRU replacement if memory is full.** :  If the memory is full, the system uses the **FIFO or LRU page replacement algorithm** to replace the page in main memory.

When a page is replaced, the evicted page is moved to swap memory, and the new page is brought from swap memory to main memory.

## Example Executable

An executable file consists of a size (in KB) and a set of commands. Each command performs an arithmetic or memory operation.

### Example:  

load 11, 1001

add 1001, 2001, 3001

print 3001

- The executable has a size of 8 KB. - The `load` command loads the value `11` into memory address `1001`. - The `add` command adds values from memory addresses `1001` and `2001`, and stores the result in `3001`. - The `print` command outputs the value stored in address `3001`.

## Replacement Algorithm

The system uses the **FIFO and LRU** page replacement algorithms for handling page swaps when memory is full.

- **FIFO :** The oldest page in memory is replaced first. Pages are managed in the order they are loaded into memory.
- **LRU :** Least recently used page is replaced first.

## Sample Usage

Below is a sample session where several processes are loaded, run, and manipulated:

Sample Command Sequence

load file1 file2 file3

run 1

pteall outfile1

pte 2 outfile1

load file4

listpr

pteall outfile1

run 2

kill 1

pteall outfile1

run 3

run 4

exit


In this session: 1. `file1`, `file2`, and `file3` are loaded into memory. 2. Process with `pid=1` is run. 3. All page tables are printed to `outfile1`. 4. Page table for process `pid=2` is appended to `outfile1`. 5. `file4` is attempted to load (if space is available). 6. Lists all active processes. 7. Process `pid=1` is killed, freeing its memory. 8. The system exits after running all remaining processes.

## Error Handling

1. **Invalid Memory Address:** If a memory address provided in a command exceeds the allocated size for a process, an error message is printed:


Invalid Memory Address **address** specified for process id **pid**


The process is terminated immediately after the invalid access.

2. **Invalid PID :** If a command is issued for an invalid PID, the system prints an error message and continues with the next command:

Invalid PID given


3. **Memory Full:** If both main memory and swap memory are full, and the system attempts to load a new executable, the following error message is shown:

filename4 could not be loaded - memory is full

## Known Issues and Limitations

- The system uses a FIFO or LRU page replacement strategy. Although this works as expected, **FIFO** may not be as efficient as **LRU (Least Recently Used)** in real-world scenarios where locality of reference is important. - All memory operations are assumed to succeed unless memory bounds are explicitly violated. The system does not handle partial loading of processes. - The page size and memory sizes must be explicitly provided as command-line arguments and cannot be dynamically changed during execution.

## Future Improvements

1. **Memory Optimization:** The system could benefit from more advanced data structures for managing memory, such as a **balanced tree** or **priority queue** for faster page replacements and allocations.

## Compilation and Execution

To compile and run the system, use the following commands:

```bash
# Compile with FIFO Page Replacement  
g++ -o fifo FIFO.cpp -std=c++11     or   make fifo

# Compile with LRU Page Replacement  
g++ -o fifo LRU.cpp -std=c++11     or   make lru

# Compile both 
make or make all

# Run the system with specified memory sizes and input/output files  
./fifo -M 32 -V 32 -P 512 -i infile -o outfile  or 
 ./lru -M 2 -V 6 -P 1024 -i infile -o outfile
```
**File Structure**
 
- FIFO.cpp or LRU.cpp : The main implementation file for the memory management system.
- README.md: This README file with details of the project, instructions, and usage.
-  infile: The input file containing commands to load and run processes.
- outfile: The output file that stores the results of system commands and process outputs.
- file1, file2, ...: Example executable files that the system loads and executes.
