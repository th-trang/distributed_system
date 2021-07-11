# CHAPTER 2: BASIC SOCKETS
## 2.1 Socket Addresses
- When initiates communication, a client must specify the IP address of the host running the server program. Then network infrastructure uses *destination address* to route the client's information.
- The *InetAddress* represents a network destination, encapsulating both names and numerical address info. It has 2 subclasses: *Inet4Address* and *Inet6Address*.
- To get the address of the local host, the program takes advantage of the *NetworkInterface* abstration. It provides access to information about all of a host's interfaces.
## 2.2 TCP Sockets
- Java provides two classes for TCP: *Socket* and *ServerSocket*.
- 
