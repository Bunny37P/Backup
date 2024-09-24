# Assignment 2 - Producer-Consumer Problem

## Overview

This assignment involves implementing inter-process communication (IPC) using the Producer-Consumer model in C. The program creates multiple processes to handle the generation and consumption of random lowercase alphabetic characters. Producers generate characters, while consumers count the number of vowels.

## Functional Requirements

1. **Process Creation**: The main program forks into Producer and Consumer processes.
2. **Character Generation**: Producers generate random lowercase alphabetic characters.
3. **Vowel Counting**: Consumers count the number of vowels read from the stream.
4. **File Writing**:
   - Each Producer writes produced characters to a file `prod_<thread_number>.txt` every minute (one character per line).
   - Each Consumer writes the cumulative vowel count to a file `cons_<thread_number>.txt` every minute.
5. **Synchronization**: Proper synchronization is required to avoid loss of characters.
6. **Implementation Language**: The program is implemented in C using IPC constructs such as pipes and threads.

## Sub-Problems

### Sub-Problem 1: Single Producer, Single Consumer
- **File**: `q_1.c`
- **Description**: Implements one Producer that generates characters and one Consumer that counts vowels.

### Sub-Problem 2: Single Producer, Multiple Consumers
- **File**: `q_2.c`
- **Description**: Implements one Producer and five Consumers.

### Sub-Problem 3: Multiple Producers, Multiple Consumers
- **File**: `q_3.c`
- **Description**: Implements five Producers and five Consumers.

### Bonus Task
- **File**: `bonus.c`
- **Description**: The Producer and Consumer processes operate in different namespaces.

## Compilation and Execution

### Makefile Commands

- **Compile all sub-problems**:
    ```bash
    make all
    ```

- **Compile individual sub-problems**:
    ```bash
    make q_<sub_problem_no>
    ```

- **Clean up executables**:
    ```bash
    make clean
    ```

### Running the Programs

- To run a specific sub-problem:
    ```bash
    ./q_<sub_problem_no>
    ```

### Bonus Execution
- To run the bonus program that utilizes namespaces:
    ```bash
    ./bonus
    ```

## Additional Notes

1. **Performance**: Each Producer generates a minimum of 1 million characters per minute. The Producers run for a maximum of 5 minutes.
2. **Resource Management**: Ensure proper cleanup of resources to prevent memory leaks.
3. **Documentation**: A comprehensive explanation of code structure and logic is provided in the code comments.
