---
published: true
---
# **TCP - The Handshake**


You must crawl before you walk! Lets start with the basics and review everyone's favorite greeting - the 3 way handsake.

## How Is A Connection Established?

- The sending side (known as the client) will send a SYN segment with the port number they want to connect to on the receiver (known as the server). This segment will also include the inital sequence number (ISN) of the client.
- The server will respond with a SYN that will include an ISN of it's own as well. The server will also acknowledge the clients SYN by sending an ACK segment with an ISN of the client plus one. A SYN will always consume one sequence number.
- The client will acknowledge the server's SYN with an ACK segment - again this will be equal to the clients SYN ISN plus one.
- The side that sends the first SYN is known to perform an _active open_. The receiver of the SYN that sends the next SYN performs a _passive open_.

![tcp.png]({{site.baseurl}}/_posts/tcp.png)


## How Is A Connection Terminated?

- Because a TCP connection is full-duplex each side must shut down independently. Usually the client will initate the closing of a TCP connection but the server can close as well. In total 4 segments are needed to close a connection.
- A connection can still be open in one direction and be closed in the other. This is known as a **_TCP half-close_**. This is basically saying _"Hey I would like to close my end of the connection - here is a FIN. But please still send data until I receive a FIN from the other side"_.
- A FIN will be sent by the side that wants to close their side of the session. This FIN will contain a sequence number of the current session. The receiver of this FIN will respond with an ACK of the sequence number plus one. A FIN consumes a sequence number just like SYN. At this point the other side will send a FIN segment to which the receiver must ACK to close the session on both ends.
- The side that sends the first FIN performs and _active close_. The side that receives that FIN performs a _passive close_.

![FIN.png]({{site.baseurl}}/_posts/FIN.png)
