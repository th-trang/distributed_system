# PROCESS SCHEDULING
- **Objective of multiprogramming**: to have some process running at all times, to maximize CPU unitlization.
- **Objective of time sharing**: to switch the CPU among proceesses so frequently that users can interact with each program while it is running.
- To meet these objectivesm the **process scheduler** selects an available process (possibly from a set of several available processes) for program execution on the CPU. For a single-process system, there will never be more than one running process, If there are more processes, the rest will have to wait until the CPU is free and can be rescheduled.
## SCHEDULING QUEUES
- As processes enter the system, they are put into a **job queue**, which consists of all processes in the system.
- The processes are residing in main memory and are ready and waiting to execute are kept on a list called **the ready queue**.
   - This queue is generally stored as a linked list.
   - A ready-queue header contains pointers to the first and final PCBs in the list.
   - Each PCB includes a pointer field that points to the next PCB in the ready queue.
- The list of processes waiting for a particular I/O device is called a **device queue**.
- **Queueing diagram**: a representation of process scheduling.
##SCHEDULERS
- The operating system must select processes from the scheduling queues. The selection process is carried out by the appropriate **scheduler**.
- Often, in a batch sys, more processes are submitted than can be executed. These processes are spooled to a mass-storage device, where they are kept for later execution.
  - The **long-term scheduler**, or **job scheduler**, selects processes from the pool and loads them into memory for execution.
  - The **short-term scheduler** or **CPU scheduler**, selects from among the processes that are ready to execute and allocates the CPU to one of them.
  - The short-term scheduler execute more frequently, at least once every 100 milliseconds.
  - The long-term scheduler execute much less frequently; minutes may seperate the creation of one new process and the next.
  - The long-term scheduler controls the **degree of multiprogramming** (the number of processes in memory). If the degree of multiprogramming is stable, then the average rate of process creation must be equal to the average departure rate of processes leaving the system.
   - Processes can be described in 2 ways:
      - **I/O-bound process**: spends more time doing I/O than doing computations.
      - **CPU-bound process**: generates I/o requests infrequently, using more time doiung computations
    - It is important that long-term scheduler select a good mix of I/O-bound process and CPU-bound process.
      - if all processes are I/O bound, the ready queue will almost always be empty, and the short-term scheduler will have little to do.
      - If all processes are CPU bound, the I/O waiting queue will almost always be empty, devices will go unused, and again the system will be unbalanced.
    
