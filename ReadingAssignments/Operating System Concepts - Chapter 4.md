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
- Support for threads provided at the user level, for **user threads**, or by the kernel, for **kernel threads**.
  - User threads are supported above the kernel threads and are managed without kernal support.
  - Kernel threads are supoorted and managed directly by the operating systen.
- A relationship must exist between user threads and kernel threads. 3 common ways of establishing:
  - Many-to-one model
  - One-to-one model
  - Many-to-many model
### 4.3.1 Many-to-one Model
- Maps many user-level threads to one kernel thread.
- Thread management is done by the thread library in user space
- The entire process will block if a thread makes a blocking system call
- Because only one thread can access the kernel, multiple threads are unable to run in parallel on multicore systems.
### 4.3.2 One-to-one Model
- Maps each user thread to a kernel thread
- Provides more concurrency than the many-to-one model by allowing another thread to run when a thread makes a blocking system call.
- Allows multiple threads to run in parallel on multiprocessors.
- **Drawback**: restiction in the number of threads supported by the system.
###  4.3.3 Many-to-Many Model
- Multiplexes many user-level threads to a small or equal number of kernel threads.
- **Advantages**
  - developers can create as many user threads as necessary.
  - when a thread performs a blocking system call, the kernel can schedule another thread for execution.
## 4.4 Thread Libraries
- Provides the programmer with an API for creating and managing threads
- 2 primary ways of implementinga thread library:
  - Providing a library entirely in user space with no kernel support.
    - All code and data structures for the library exist in user space (Invoking a function in the library results in a local function call in user space and not a system call).
  - Implement a kernel-level library supported directly by the OS. 
    - Code and data structures for the lib exist in kernal space. Invoking a function in the APU for the library typically results in a sys call to the kernel.
- 3 main thread libraries:
  - POSIX Pthreads: provides as either a user-level or a kernel-level lib
  - Windows: is a kernel-lib available on Windows systems
  - Java: using a thread lib available on the host sys (on Windows sys, Java threads uses the Windows API, on UNIX and Linux use Pthreads).
