# **All About ARP**

In today's article we will be discussing the Address Resolution Protocol, better known as ARP! ARP plays a key role in almost any type of network. If you are browsing the internet today there is a high chance ARP was involved in that process. Did you know that there are different types of ARP with different functions? Well hopefully after reading this you will gain some insight into the art of ARP!

## Address Resolution Protocol - ARP

- Address Resolution Protocol is used to discover the physical MAC address of a host when the layer 3 network address is known. ARP is a layer 2 (data link) level protocol. We need ARP because even though the MAC address is unique to a host, the IP address could still change. For example let's say you had the IP address of Host A noted as 192.168.1.1. Well what if Host A's IP then changed to 192.168.1.2? How would you know where Host A is on the network now? This is why the MAC address msut be mapped to the IP address using ARP.

- ARP gathers information using a few different speaking tools. These are called ARP Reply and ARP Broadcast. An ARP Broadcast is a message sent out to the destination of FF:FF:FF:FF:FF:FF to everyone on the local subnet. This broadcast message is basically saying "Hey what is the MAC address associated with 192.168.1.1?". Hosts that do not have that IP address wil discard but the 192.168.1.1 host will use an ARP Reply and say "Hey my MAC address is AB:CD:EF:01:23:45 I am 192.168.1.1". The sender of the ARP Broadcast will receive this reply and update it's ARP Table with this new information. Now going forward the host will know the MAC address of the host associated with 192.168.1.1. 

- The ARP Table will contain the mapping of the MAC address to the IP address as well the interface it was learned on and an expiration timer. Thr timer is a countdown and once it reaches 0 the entry will be flushed out of the ARP Table. This allows ARP entries to not become stale and to constantly keep up to date incase of IP network changes.

## Reverse Address Resolution Protocol - RARP

- Reverse Address Resolution Protocol is used by certain hosts that by do not know their IP address and need to get it from a RARP server. The RARP server must be configured with the mapping of the MAC address of the host to an available IP address. The host will send a RARP broadcast message with their MAC address as the source. The RARP server will receive the broadcast and send a RARP reply with the IP address of the host. RARP is rarely used in todays networks as we have protocols such as DHCP in play now.

## Gratuitous Address Resolution Protocol

- Gratuitous Address Resolution Protocol is used by a host to find it's own IP address on the network. Gratuitous ARP is essentially a method for duplicate IP detection. It is also a way to update hosts on the network with it's updated MAC-IP mapping. A host will send a broadcast message out with it's own IP as the soruce and destination. If an ARP reply is returned with it a source IP matching it's own, then there is a duplicate IP on the network. The source and destination IP address in the GARP broadcast will be the same since it is from the local host.

## Proxy Address Resolution Protocol

- Proxy Address Resolution Protocol is a technique used to answer ARP requests on the behalf of another host. This Proxy ARP is typically used in scenarios where hosts are in the same IP space but not the same data link layer. A router will usually be the boarder or bridge between the hosts. When an ARP request is sent for a host on another data link the router reply with it's MAC address and forward & reply to requests for the IP address. Thus allowing the datagrams to be sent between the hosts.