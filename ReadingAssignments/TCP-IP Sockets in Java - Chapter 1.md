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
 
         
  

  
