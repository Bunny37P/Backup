# Assignment_2 - Producer-Consumer Problem

## Overview

This assignment involves implementing inter-process communication (IPC) using the Producer-Consumer model. The program forks multiple processes to handle the production and consumption of random lowercase alphabetic characters. Producers generate these characters, while consumers count the number of vowels read.

## Functional Requirements

1. The main program forks into Producer and Consumer processes.
2. The Producer generates random lowercase alphabetic characters.
3. The Consumer counts the vowels read from the stream.
4. Each Producer writes produced characters to a file `prod_<thread_number>.txt` (one character per line) every minute.
5. Each Consumer writes the cumulative vowel count to a file `cons_<thread_number>.txt` every minute.
6. Synchronization is maintained to avoid loss of characters.
7. The program is implemented in C using IPC constructs such as pipes.

## Sub-Problems

### Sub-Problem 1: Single Producer, Single Consumer

- **File**: `q_1.c`
- **Description**: Implements one producer that generates characters and one consumer that counts vowels.
- **Execution**: To run this program, compile it with `make q_1` and execute `./q_1`.

### Sub-Problem 2: Single Producer, Multiple Consumers

- **File**: `q_2.c`
- **Description**: Implements one producer that generates characters and five consumers that count vowels.
- **Execution**: To run this program, compile it with `make q_2` and execute `./q_2`.

### Sub-Problem 3: Multiple Producers, Multiple Consumers

- **File**: `q_3.c`
- **Description**: Implements five producers that generate characters and five consumers that count vowels.
- **Execution**: To run this program, compile it with `make q_3` and execute `./q_3`.

## Compilation and Execution

### Makefile Commands

- **Compile all sub-problems**:
  ```bash
  make all
