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
