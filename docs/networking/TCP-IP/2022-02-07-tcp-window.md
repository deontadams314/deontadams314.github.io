# **The TCP Window**

The Window Scale option is a TCP option used in modern TCP implementations. The maximum number of bytes allowed to be sent at once is 65,535. This is a problem and does not provide adequate traffic flow in todays networks. The problem to solve is todays topic - the window scale option!

## What is a TCP Window?

- The TCP window is the maximum number of bytes that can be sent before an ACK is received. What does this mean exactly? Well both the client and server in a TCP connection will advertise in the SYN segment their window size. This is a buffer that the sender or receiver will use to determine how much data they can send/receive. The max number for the window size is 65,535. However if the TCP window scale is used this can be multiplied to a larger scale depending on what was set in the SYN segment. A TCP window is dynamic the size can increase or decrease within a TCP connection.

## What is Window Scaling?

- Window scaling is a TCP option used to increase the flow of data in a TCP connection. As an option Window scaling is set in the SYN segment and advertised to the other side of the connection. Window scaling takes the window scale size and multiplies by a multiplier. This number is actual window for the send or receive buffer.

## What is a Sliding Window?

- A sliding window allows the sender to transmit multiple segments within a given window size without receiving an ACK. The sliding window also keeps track of data ACK'd, data not ACK'd all in the availble window size. As data is ACK'd the window slides to the right depending on how fast it is consumed by the other end.
