# CHAPTER 1: INTRODUCTION

## 1.1. Network, Packets and Protocols
- A computer network consists of machines interconnected by communication. Those machines are *hosts* and *routers* 
  - **Hosts** are computer that run applications. The application programs running on hosts are thr real "users" of the network.
  - **Routers** are machines whose job is to relay (or forward) *information* from 1 communication channel to another.
  - **A Communication channel** is a means of conveying sequences of bytes from one host to another, may be wired (Ethernet), may be wireless (Wifi) or other connections.
  - **Information**: sequences of bytes that are constructed and interpreted by programs.
    - Those sequences, in the context of computer networks, are generally called *packets*.
      - Packets contains control info and sometimes includes user data. Routers use control info to figure our how to forward each packet.
  - **Protocol**: an agreement about the packets exchanged by communicating programs and what they mean
    - Tells how packets are structured (ex: where the dest info is located in the packet, how big and how to interprete those info).
    - Is designed to solve a specific prob using given capabilities.
- **TCP/IP (Transmission Control Protocol/Internet Protocol)**: a collection of protocols used in the Internet to implement a useful network. The main protocols in the TCP/IP suite are the *Internet Protocol (IP)*, the *Transmission Control Protocol (TCP)* and the *User Diagram Protocol (UDP)*.
- In TCP/IP, the bottom layer consists of the underlying communication channels (ex: Ethernet or dial-up modem connections). Those channels are used by the *network layer*, which deals with the problem of forwarding ackets towards their destination. The single network layer protocol in the TCP/IP suite is the Internet Protool, it solves the problem of making the sequence of channels ans routers between any two hosts.
- The Internet Protocol provides a *datagram* service: every packet is handled and delivered by the network independently. To make it work, each IP packet has to contain the *address of its destination*. But it can occasionally lose, reorder or duplicate packets in transit through the network.
- The layer above IP is called the *transport layer*. It offers a choice between 2 protocols: TCP and UPD.
  - Each provides different kind of transport for different needs.
  - Both have addresses to identify applications within hosts called *port number*.
  - Both are called *end-to-end transport protocols* because they carry data all the way from one program to another
  - *TCP* provides *reliable byte-stream channels* because it is designed to detect and recover from the losses, dupliation and other errors that may occur in the host-to-host channel. It is a *connection-oriented protocol*: beofore using it to communicate, two programs must first establish a TCP connection, which involves completing an exchange of *handshake messages* between the 2 communicating computers.
  - *UDP* does not attempt to recover from errors, it simply ectends the IP best-effort-datagram service so that it works between application programs.
## 1.2 About Addresses
- Before a program can communicate with another program, there must be sth to identify the other program. It takes two pieces of information: an *Interent addresses* used by IP, and a *port number*.
- **Internet Addresses** are binary numbers. They come in 2 versions:
  - *Version 4 (IPv4)*: 32 bits long, written as a group of four decimal numbers seperated by periods (or *dotted-quad*). The four numbers in a dotted-quad string represent the contents of four bytes of the Internet address - thus, each is a number bwtween 0 and 255 (ex: 10.1.2.3)
  - *Version 6 (IPv6)*: 128 bits long, represented as groups of hexadecimal digits, seperated by colons (ex: 2000:fdb8:0000:0000:0001:00ab:853c:39a1). Each group of digits representes two bytes of the address, leading zeros may be obmitted. Consecutive groups that contain only zeros may be obmitted altogether but this can only done once in any address. (ex: 2000:fdb8::1:00ab:853c:39a1).
- The Internet address is the street address whereas thr port corresponds to the room number. Port nummbers are 16-bit unsigned binary numbers, so each one is in the range 1 to 65,535 (0 is reserved).
- Cetain special-purpose addresses are defined
  - **Loopback interface**, a virtual device that simply echoes transmitted packets right back to the sender. It is useful for testing because packets sent to that addr. are immediately returned back to the destination. It is present on every host and can be used when computer has no connection to the network. The loopback address for IPv4 is *127.0.0.1*, for IPv6 is *0:0:0:0:0:0:0:1*
  - **Private use**: start with 10 or 192.168, as well as those whose first number is 172 and whose second number is between 16 and 31, applied for IPv4 addresses. They were originally designated for private networks, often used in home and small offices that are connected to the Internet through a *network address translation (NAT)* device.
  - **Link-local** or **autoconfiguration** addresses. For IPv4, addresses begin with 169.254. For IPv6, any addresses whose first 16-bit chunk starts with FE8. Such addresses can only be used for communication between hosts connected to the same network, routers will not forward them.
  - **Multicast addresses**: Whereas regular IP (sometimescalled “unicast”) addresses refer to a single destination, multicast addresses potentially refer to an arbitrary number of destinations. In IPv4, multicast addresses in dotted-quad format have a first number inthe range 224 to 239. In IPv6, multicast addresses start with FF.
## 1.3 About Names
- Internet protocols deal with addresses (binary numbers), not names. The use of names is a convenience feature for couple of reasons:
  - Names are easier for humans to remember that dotted-quads (IPv4) or hexadecimal digits (IPv6)
  - Names provide a level of indirection, which insulates users from IP addresses changes.
- The name-resolution service can access info from a wide variety of sources. 2 primary sources are
  - The *Domain Name System (DNS)*: a distributed database that maps *domain names* to Internet addresses and other info. DNS protocol allows hosts connected to the Internet to retrieve info from that database using TCP or UDP.
  - *Local configuration databases* are generally OS-specific mechanisms for local name-to-Internet address mappings.
 
         
  

  
