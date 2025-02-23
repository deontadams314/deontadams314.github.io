# **OSPF Neighbor States**

OSPF is a rather complex routing protocol in the network world. Known as a link state routing protocol, OSPF maintains a link state database which is basically a topology of the network. OSPF routers have many states which they go through within the process of discovering peers, electing DR and BDRs and forming adjacensies. Here we will discuss these states which could possibly help you in the future if you ever had to troubleshoot them.

## Down

- This is the initial OSPF state. In this form Hello messages have not been received from a peer. However they may be sent in this state.

## Attempt

- This state is only valid in Non-Broadcast Multi Access (NBMA) netwoks where neighbors are manually configured. Hellos are sent to a neighbor at the HelloInterval interval timeframe.

## Init

- In this state a Hello packet has been received from the neighbor but the recieving router has not seen its RID in the message. If a receiver sees it's own RID in the hello message, this is seen as an ACK that their hello message has been received by its peer.

## 2-Way

- Bi-directional communication has been established in this state (each router has seen the others hello message). This is where the router decides if a full adjacency will be formed with its neighbor.

- OSPF routers only form full adjacencies with the Designated Router (DR) and Backup Designated Router (BDR) in broadcast and  NBMA networks. The router will stay in the 2-Way state with all other neighbors.

- In broadcast and NBMA networks the DR & BDR are elected at the end of this state.

## ExStart

- In this state routers from a master/slave relationship and determine the inital Database Description number. This will be used for the exchange of the Database Description packets. The router with the highest RID becomes the master.

## ExChange

- In this state Database Description packets are exchanged which describe the link state database. Link state request packets can also be sent to request recent LSAs 

## Loading

- In this state the routers send Link State Request (LSR) packets to neighbors requesting more recent LSAs that have been discorved in the ExChange state but not yet recieved by the peer. Link State Updates (LSU) are sent to update any missing LSAs.

## Full

- OSPF neighbors in this state are fully adjacent. All the router and network LSA's are exchanged with the LSD synchronized.