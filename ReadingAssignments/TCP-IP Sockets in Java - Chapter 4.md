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
 - In either case, the new thread does not begin execution until it **start()** method is invoked.
### 4.1.2 Server Protocol
- Since the multitasking server approaches we are going to describe are independent of the particular client-server protocol, we want to be able to use the same protocol implementation for both. The code for the echo protocol is given in the class **EchoProtocol**. This class encapsulates the per-client processing in the static method **handleEchoClient()**.
- **Logger** class: a logging facility that maybe local or remote. Through an instance of this class, we can record the various server activities as shown in **EchoProtocol**. You may use several loggers in your server, each serving a different purpose and potentially behaving in a different way.
- **Level** class: encapsulates the notion of the importance of messages. Each instance of **Logger** has a current level, and each message logged has an associated level; messages with levels below the instance's current level are discarded.
### 4.1.3 Thread-per-Client
- In a *thread-per-client server*, a new thread is created to handle each connection. The server
executes a loop that runs forever, listening for connections on a specified port and repeatedly
accepting an incoming connection from a client and then spawning a new thread to handle
that connection.
### 4.1.4 Thread Pool
- Every new thread consumes system resources: spawning a thread takes CPU cycles and each thread has its own data structures (e.g., stacks) that consume system memory. In addition, when one thread blocks, the JVM saves its state, selects another thread to run, and restores the state of the chosen thread in what is called a context switch. As the number of threads increases, more and more system resources are consumed by thread overhead. Eventually, the system is spending more time dealing with context switching and thread management than with servicing connections. At that point, adding an additional thread may actually increase client service time.
- We can avoid this problem by letting the server creates a *thread poo*l on start-up by spawning a fixed number of threads. 
  - When a new client connection arrives at the server, it is assigned to a thread from the pool. 
  - When the thread finishes with the client, it returns to the pool, ready to handle another request. 
  - Connection requests that arrive when all threads in the pool are busy are queued to be serviced by the next available thread.
### 4.1.5 System-Managed Dispatching: The Executor Interface
The interface Executor represents an object that executes Runnable instances according to some strategy, which may include details about queueing and scheduling, or how jobs are selected for execution.
## 4.2 Blocking and Timeouts
### 4.2.1 accept(), read(), receive()
- For these methods, we can set a bound on the maximum time (in milliseconds) to block, using the **setSoTimeout()** method of *Socket*, *ServerSocket*, and *DatagramSocket*. If the specified time elapses before the method returns, an *InterruptedIOException* is thrown. For Socket instances, we can also use the **available()** method of the socket’s *InputStream* to check for available data before calling **read()**.
