# Chapter 3
## Process Concept
### The Process
- The process is a program in execution
- The memory layout of a process is typically divided into multiple sections:
  - Text section
  - Data section
  - Heap section
  - Stack section
- The sizes of the text and data sections are fixed. The stack and heap sections can shrink and grow dynamically during program execution.
### Process State
- As a process executes, it changes states. A process maybe in one of the following states:
  - New
  - Running
  - Waiting
  - Ready
  - Terminated
### Process Control Block
- Process Control Block  is the kernel data structure that represents a process in an operating system.
- It contains many pieces of information associated with a specific process, including these:
  - Process state
  - Program counter
  - CPU registers
  - CPU-scheduling information
  - Accounting information
  - I/O status information
## Process Scheduling
### Scheduling Queues
- As processes enter the system, they are put into a ready queue, where they are ready and waiting to execute on a CPU's core. This queue is generally stored as a linked list.
- Processes that are waiting for a certain event to occur placed in a wait queue.
### CPU Scheduling
- The role of the CPU scheduler is to select from among the processes that are in the ready queue and allocated a CPU core to one of them.
- Swapping is an intermediate form of scheduling, where a process is removed from memory and thus reduce the degree of multiprogramming. Later, the process can be reintroduced into memory and its execution can be continued where it left off.
## Context Switch
- An operating system performs a context switch when it switches from running one process to running another.
- Context-switch times are highly dependent on hardware support.
## Operations on Process
### Process Creation
   The fork() and CreateProcess() system calls are used to create processes on UNIX and Windows systems, respectively.
### Process Termination
   A process terminates when it finishes executing its final statement and asks the operating system to delete it by using the exit() system call.
