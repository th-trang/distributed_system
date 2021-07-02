# Chapter 4: Threads
## 4.1 Overiew
- A thread is a basic unit of CPU utilization; it comprises a thread ID, a program counter, a register set and a stack.
- It shares with other threads belonging to the same process its code section, data section and other operating-system resources.
- A traditional process has a single thread of control. If a process has multiple threads of control, it can perform more than one task at a time.
### 4.1.1 Motivation
- Most software applications that run on modern computers are multithreaded.
- An application is implemented as a seperate process with several threads of control.
  - **Ex**: A web browser might have one thread display images or text while another thread retrieves data from the network.
- Process creation is time comsuming and resource intensive. It is generally more efficient to use one process that contains multiple threads. 
  - If the web-server process is multithreaded, the server will create a seperate thread that listens for client requests. When a request is made, rather than creating another process, the server creates a new thread to service the request and resume listening for additional requests.
- Threads play a vital role in **remote procedure call (RPC)** systems.
  - When a server receives a message, it services the message using a separate thread. This allows the server to service several concurrent requests.
- Most operating-system kernels are now multithreaded. Several threads operate in the kernel, and each thread performs a specific task.
### 4.1.2 Benefits
- The benefits of multithreaded programming can be broken down into 4 categories:
  - **Responsiveness**: Multithreading an application may allow a program to continue running even if part of it is blocked or is performing a lengthy operation, thereby increasing responsiveness to the user.
  - **Resource sharing**: Processes can only share resources through techniques such as shared memory and message passing and must be arranged by the programmer. The benefit of sharing code and data is that it allows an application to have several different threads of activity within the same address space.
  - **Economy**:  it is significantly more time consuming to create and manage processes than threads.
  - **Scalability**: threads may be running in parallel on different processing cores. A single-threaded process can run on only one processor, regardless how many are available.
## 4.2 Multicore Coding
- In respond to the need for more computing performance, multiple computing cores are placed on a single chip. Each core appears á a seperate processor. We call **system multicore** or **multiprocessor systems**.
### 4.2.1 Programming Challenges
- There are 5 areas present challenges in programming for multicore systems:
  - Identifying tasks
  - Balance
  - Data splitting
  - Data dependency
  - Testing and debugging
### 4.2.2 Types of Parallelism
There are 2 types:
  - Data parallelism: distributing subsets of the same data across multiple computing cores and performing the same operation on each core.
  - Task parallelism: distributing tasks (threads) across multiple computing cores.
## 4.3 Multithreading Models
