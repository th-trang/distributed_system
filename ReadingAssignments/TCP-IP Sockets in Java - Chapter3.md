#CHAPTER 3: SENDING AND RECEIVING DATA
## 3.1 Encoding Information
- Bytes of infomation can be transmitted through a socket by writing them to an **OutputStream (associated with a Socket)** or encapsulating them in a **DatagramPacket (which is then sent via a DatagramSocket)**. However, the only data types to which these operations can be applied are bytes and arrays of bytes. Therefore, all variable types (ints, longs, chars,...) must be converted to byte arrays.
- *Bitmaps* are a very compact way to encode boolean information. 
  - The idea of bitmap is that each of the bits of an integer type can encode one boolean value - 0 representing false and 1 representing true.
## 3.2 Composing I/O Streams
- Java's stream classes can be composed to provide powerful capabilities.
  - We can wrap the **OutputStream** of a **Socket* instance in a **BufferedOutputStream** instance to improve performance by buffering bytes temporarily and flushing them to the underlying channel all at once.
   - We can then wrap that instance in a **DataOUtputStream** to send premitive data types.
--------------------------------------------------------------------------------------------------------
       Socket socket = new Socket (server, port);
       DataOutputStream out = new DataOutputStream(new BufferedOutputStream(socket.getOutputStream()));
-------------------------------------------------------------------------------------------------------
## 3.3 Framing and Parsing

