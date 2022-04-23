---
published: true
---
# **NetSec: ARP Spoofing**

In todays article in the NetSec series we will be discussing another layer 2 network attack, ARP Spoofing. ARP Spoofing also goes by the name ARP Cache Poisoning/ARP Poisoning. To understand how an ARP Spoofing attack works we must understand how Address Resolution Protocol (ARP) functions. I won't talk too much here, let's dive in!

## How does ARP work?

Address Resolution Protocol allows a host to find another host on a network. Before a host can send a layer 3 packet to a destination they must have the MAC address of the destination host. To simply put ARP translates IPv4 addresses to MAC addresses. Every host on a network maintains an ARP cache which contains the mappings of IP addresses to MAC addrreses and the interface used to reach that host. If a host doesn't know the MAC address for a certain IP, an ARP broadcast message is sent on the network asking "Who does this IP belong to?". The host who has the IP address will respond with it's MAC address and that will be captured in the requesters ARP cache. ARP unfortunately does not have any built in security mechanisms. This would allow anyone to respond to an ARP request with no way to verify if the information is correct. ARP also allows hosts send ARP replies without it even being requested. These two downfalls is what allows ARP Spoofing attacks to work and wreck havoc on a network.

## What is ARP Spoofing?

ARP Spoofing is a layer 2 Man In The Middle (MitM) Attack that takes advantage of the lack of security in the ARP protocol. In order for ARP Spoofing to work an attacker must already have access on the network. Once on the network the attacker would identify a host or hosts on the network and use a tool to forge ARP responses. These reponses would claim the attackers MAC address as the MAC address of the target host(s). Other devices on the network would have no way to verify this and simply update their ARP cache with the MAC address of the attacker. At this point the attacker may inspect the packets being sent while forwarding to the actual destination to avoid detection. They may even steal information from the packets that have recieved or modify the data.

## How can I detect an ARP Spoofing attack?

A host can detect ARP Spoofing on an network by checking and verifying the ARP cache on your machine. If you see the same MAC address on different IP addreses this could be a sign of ARP Spoofing taking place. Using WireShark to sniff the traffic on your network can also determine patterns and help you find a potential spoofer.

## Mitigation Techniques

There are a few ways that a network admin can fight against ARP Spoofing
- Static ARP Entries
    - Use static ARP entries for critical hosts (DNS servers, routers, load balancers etc.). This however does not scale on a large network as the entries would need to be entered mantained on each host on the network.
- OS Security Settings
    - Each OS behaves differently and has built in defense settings that can be used to combat ARP Spoofing.
- ARP Detection & Prevention Software 
    - 3rd party software can be put in place on host machines to detect ARP Spoofing
- Packet Filtering 
    - Use packet filtering to verify if packets contain conflicting source information.

## How do hackers perform this attack?

There are a multiple tools an attacker can use to spoof ARP responses. A few include:
    - ARPspoof
    - Arpoision
    - Cain and Abel
