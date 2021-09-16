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
### 4.2.2 Connecting and Writing
- The Socket constructor attempts to establish a connection to the host and port supplied as arguments, blocking until either the connection is established or a system-imposed timeout occurs. Unfortunately, the system-imposed timeout is long, and Java does not provide any means of shortening it. To fix this, call the parameterless constructor for *Socket*, which returns an unconnected instance. To establish a connection, call the **connect()** method on the newly constructed socket and specify both a remote endpoint and timeout (milliseconds).
- A **write()** call blocks until the last byte written is copied into the TCP implementation’s local buffer; if the available buffer space is smaller than the size of the write, some data must be successfully transferred to the other end of the connection before the call to **write()** will return. Thus, the amount of time that a **write()** may block is ultimately controlled by the receiving application.
### 4.2.3 Limiting Per-Client Time
Suppose we want to implement the Echo protocol with a limit on the amount of time taken to service each client. The protocol instance keeps track of the amount of time remaining, and uses **setSoTimeout()** to ensure that no **read()** call blocks for longer than that time.
## 4.3 Multiple Recipients
### 4.3.1 Broadcast
With broadcast, all hosts on the (local) network receive a copy of the message.
### 4.3.2 Multicast
With multicast, the message is sent to a multicast address, and the network delivers it only to those hosts that have indicated that they want to receive messages sent to that address.
## 4.4 Controlling Default Behaviors
### 4.4.1 Keep - Alive
- TCP provides a keep-alive mechanism where, after a certain time of inactivity, a probe message is sent to the other endpoint. If the endpoint is alive and well, it sends an acknowledgment. After a few retries without acknowledgment, the probe sender gives up and closes the socket, eliciting an exception on the next attempted I/O operation.
- By default, keep-alive is disabled. Call the **setKeepAlive()** method with true to enable keep-alive.
### 4.4.2 Send and receive Buffer Size
- The **getReceiveBufferSize()**, **setReceiveBufferSize()**, **getSendBufferSize()**, and **setSendBufferSize()** methods get and set the size (bytes) of the receive and send buffers.
- The **getReceiveBufferSize()** and **setReceiveBufferSize()** methods get and set the size (bytes) of the receive buffer for *Socket* instances created by the **accept()**.
### 4.4.3 Timeout
- We can specify a maximum blocking time for the various operations.
- The **getSoTimeout()** and **setSoTimeout()** methods get and set the maximum time (milliseconds) to allow read/receive and accept operations to block. A timeout of 0 means the operation never times out. If the timeout expires, an exception is thrown.
### 4.4.4 Address Reuse
- Under some circumstances, you may want to allow multiple sockets to bind to the same socket address. To enable this, you must allow address reuse.
- The **getReuseAddress()** and **setReuseAddress()** methods get and set reuse address permissions. A value of true means that address reuse is enabled.
### 4.4.5 Eliminating Buffering Delay
- TCP attempts to help you avoid sending small packets, which waste network resources. It does this by buffering data until it has more to send. While this is good for the network, your application may not be so tolerant of this buffering delay. You can disable this behavior.
- The **getTcpNoDelay()** and **setTcpNoDelay()** methods get and set the elimination of buffering delay. A value of true means that buffering delay is disabled.
### 4.4.6 Urgent Data
- TCP includes the concept of urgent data that can (theoretically) skip ahead. Such data is called out-of-band because it bypasses the normal stream.
- To send urgent data, call the **sendUrgentData()** method, which sends the least significant byte of the int parameter. To receive this byte, the receiver must enable out-of-band data by passing true to **setOOBInline()**. The byte is received in the input stream of the receiver.
