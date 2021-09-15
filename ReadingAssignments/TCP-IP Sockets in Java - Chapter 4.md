# CHAPTER 4: BEYOND THE BASICS
## 4.1 Multitasking
- *Iterative server*: a server that handles clients sequentially, finishing with one client before servicing the next.
  -  If a client connects while another is already being serviced, the server will not echo the new client's dât until it has finished with the current client.
  -  Works best for applications where each client requires a small, bounded amount of server connection time.
 - *Java threads*: a mechanism allowing servers to handle many clients simultaneously. Each connection proceeds independently without interfering with other connections.
### 4.1.1 Java Threads
- Java provides two approaches for performing a tast in a new thread:
  1) Defining a subclass of the **Thread** class with a **run()** method that performs the task, and instantiating it. This approach can only be used for classes that do not already extend some other class.
  2) Defining a class that implements the **Runnable** interface with a **run()** method that performs the task and passing an instance of that class to the **Thread** constructor. This approach is always applicable.
-----------------------
  interface Runnable {
    - void run();
  }
------------------------
 - In either case, the new thread does not begin execution until it **start()** method is invoked.
