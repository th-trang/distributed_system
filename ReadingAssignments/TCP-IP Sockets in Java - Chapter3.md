#CHAPTER 3: SENDING AND RECEIVING DATA
## 3.1 Encoding Information
- Bytes of infomation can be transmitted through a socket by writing them to an **OutputStream (associated with a Socket)** or encapsulating them in a **DatagramPacket (which is then sent via a DatagramSocket)**. However, the only data types to which these operations can be applied are bytes and arrays of bytes. Therefore, all variable types (ints, longs, chars,...) must be converted to byte arrays.
- *Bitmaps* are a very compact way to encode boolean information. 
  - The idea of bitmap is that each of the bits of an integer type can encode one boolean value - 0 representing false and 1 representing true.
## 3.2 Composing I/O Streams
- Java's stream classes can be composed to provide powerful capabilities.
  - We can wrap the **OutputStream** of a **Socket** instance in a **BufferedOutputStream** instance to improve performance by buffering bytes temporarily and flushing them to the underlying channel all at once.
   - We can then wrap that instance in a **DataOUtputStream** to send premitive data types.
--------------------------------------------------------------------------------------------------------
       Socket socket = new Socket (server, port);
       DataOutputStream out = new DataOutputStream(new BufferedOutputStream(socket.getOutputStream()));
-------------------------------------------------------------------------------------------------------
## 3.3 Framing and Parsing
- Framing refers to the problem of enabling the receiver to locate the beginning and end of a message. Whether information is encoded as text, as multibyte binary numbers, or as some combination of the two, the application protocol must specify how the receiver of a message can determine when it has received all of the message.
- For messages sent over TCP sockets, the situation can be complicated because TCP has no notion of message boundaries. If the fields in a message all have fixed sizes and the message is made up of a fixed number of fields, then the size of the message is known in advance and the receiver can simply read the expected number of bytes into a byte[] buffer.
- Two general techniques enable a receiver to unambiguously find the end of the message:
  - *Delimiter-based*: The end of the message is indicated by a unique marker, an explicit byte sequence that the sender transmits immediately following the data. The marker must be known not to occur in the data.
  - *Explicit length*: The variable-length field or message is preceded by a (fixed-size) length field that tells how many bytes it contains.
## 3.4 Java-Specific Encodings
When you use sockets, generally either you are building the progeams on both ends of the communication channe;, or you are communicating using a given protocol. When you know that (i) both ends of the commnunication will be implemented in Java, and (ii) you have complete control over thr protocol, you can make use of Java's built-in facilities like the Serializable interface or the Remote Method Invocation (RMI) facility. RMI lets you invoke methods on different Java virtual machines, hiding all the messy details of arguments encoding and decoding. Serialization handles conversion of actual Java objects to byte sequences for you, so you can transfer actual instances of Java objects between virtual machines.
