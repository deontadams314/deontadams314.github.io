---
published: true
---
# **BGP States**

## INTRO

- A BGP speaker has various states that it goes through before a neighbor adjacency is fully made. A finite state mechanism (FSM) is used to manage the states of each BGP peer during this process. FSM is a set of limited states that a BGP speaker is allowed to exist in during this process. BGP uses TCP for its connections so speakers listen on port 179.

- The first 3 states deal with the TCP side of the connection:
	- IDLE, CONNECT, ACTIVE
- The other 3 deal with BGP application side:
	- OPENSENT, OPENCONFIRM, ESTABLISHED

- Here we will discuss the many BGP states and hopefully you can walk away understanding the in's and out's of this process.

## IDLE

- The IDLE state is the first stage of the BGP neighbor process. In this state the BGP speaker has been configured and is waiting for a start event. The speaker is basically waiting for a TCP connection to begin. Once started the speaker will transition into the CONNECT state.

## CONNECT

- In the CONNECT state the BGP speaker is simply waiting for the TCP connection to be completed.
- If the TCP connection is succesfull the speaker transitions into the OPENSENT state, where the OPEN message is sent.
- If the TCP connection fails it will instead move into the ACTIVE state.
- If the ConnectRetry timer expires the connection will remain in the CONNECT state.

## ACTIVE

- In the ACTIVE state the BGP speaker is listening for a BGP peer and trying to accept a TCP connection.
- If the TCP connection is successfull the speaker will transition into the OPENSENT state, where the OPEN message is sent.
- If the ConnectRetry timer expires the router will move back to the CONNECT state.
- If a device is stuck in the ACTIVE and CONNECT states usually this indicates a TCP issue and could be related to a firewall blocking the TCP port 179.

## OPENSENT

- In the OPENSENT state is where the OPEN message will be sent and the speaker is also waiting to receive an OPEN message from its peer.
- The OPEN message is used to establish BGP peering connections and contains the following parameters
		- BGP Version: The version of BGP used by the speaker
		- AS #: Autonomous System # of the BGP speaker
		- Hold Timer: The max time that can pass before a peer is declared dead. Once a keep alive 			 is received if a response exceeds the hold timer the peer is considered dead. The lower     	   of the two BGP speakers hold timers is used. 3 sec is the default.
		- BGP ID - Identifier of the BGP speaker
        - Optional - optional BGP parameters
- If the OPEN message contains no errors a KEEPALIVE message is sent and the speaker transitions into the OPENCONFIRM state.
- If the OPEN message has errors the state moves back to IDLE.

## OPENCONFIRM

- In the OPENCONFIRM state the BGP speaker will wait for a KEEPALIVE. Once received it will transition into the ESTABLISHED state and the neighbor negotiation is sleep.
- If a NOTIFICATION error message is recieved then the state moves back into IDLE.

## ESTABLISHED

- In the ESTABLISHED state is the final stage in the BGP process. At this point BGP update messages are shared between speakers as well as KEEPALIVES. 
- The KEEPALIVE messages essentially check if a speaker is there and will reset the hold timer. If the hold timer expires the peer is considered dead and the state is moved back to IDLE.
- Any error or NOTIFICATION message will result in the speaker moving back into the IDLE state.
