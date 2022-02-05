---
published: true
---
# **TCP - Half-Close and Half-Open**

Half-close and Half-open, what is this? And no these are not sequels in the Half-Life series =) - but rather TCP features that can occur due to its Full-Duplex nature. Here I will give you a few details about these two features so you can know the difference.

## Half-Close

- A TCP half-close occurs when one side of the TCP connection closes it's side of the connection but can still receive data from the other end. A FIN is sent by the closing side and the receiver will ACK the FIN.

- Using a half-close has been looked at as being unreliable if needed for an extended period of time. This is because some devices like firewalls implement half-close timeouts. If the final FIN is not received within the timeout period the connection is then closed. 

![half-close.png]({{site.baseurl}}/assets/images/half-close.png)

## Half-Open

- A TCP half-open occurs when one of side of the TCP connection has crashed or forcibly closed without the otherside being notified. As long as no data is received the side that is till up will never know the other side is closed. Common causes for half-open's are device being powered off during a TCP connection.
