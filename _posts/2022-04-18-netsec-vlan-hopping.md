---
published: true
---
# **NetSec: VLAN Hopping**

Welcome to the first part of a series that I figure most of you will love. In the NetSec series we will take a look a different network security concepts. This will include offense, defense, mitgation network security techniques. We will explore how it works and how we can defend against network attacks. The first concept of the NetSec series we will dive into is VLAN hopping.

## What is VLAN Hopping?

VLAN hopping is a network security attack where an attacker can gain access to traffic on a VLAN from another VLAN on the same network that might not necessarily be able to talk to each other. In order to take advantage of VLAN hopping an attacker must first breach one VLAN. Imagine a scenario where an attacker has access to a VOIP VLAN. They could potentially VLAN hop to your management VLAN or even a database VLAN with secret classified information. There are two ways to start a VLAN hopping attack, switch spoofing and double tagging.

## Switch Spoofing

Switch Spoofing is where an attacker takes advantage of Dynamic Trunking Protocol packets to negotiate a trunk port on a switch. By default switch ports are configured as dynamic auto or dynamic desirable. This will mean they will prefer the option to negotiate a trunk with another switch. Attackers take advantage of this by simply pluging their computer into a port and negotiate trunk link. At this point the attacker would have access to all VLANs on the network. Avoid configuring switch ports with the dynamic trunk options.

## Double Tagging

Double Tagging is where an attacker uses 802.1Q tagging in order to attack a VLAN. The attacker connected to a 802.1Q enabled port will send frames with an inner and outer VLAN tag. The outer tag is the actual VLAN the attacker is in. While the inner tag is the VLAN where the attacker wants to send the frame. The frame is able to be forwarded without the outer tag because it is the native vlan of the interface. This means the frame is sent to the target as if it is on the destination VLAN. This is a one way attack (good for DDOS attacks) and is only possible due to a switch using the native VLAN.

## Mitigation Techniques

Switch Spoofing
    - Switch ports should never be configured as dynamic switch ports.
    - Instead configure trunk ports with the "nonegotiate" option.   
    - Ensure any port not meant to be a trunk port is configured as an access port.

Double Tagging
    - Do not put any host onto VLAN 1 (the default native VLAN).
    - Change the native VLAN on any trunk port to an unused VLAN on the network.

## How do hackers perform this attack?

- Attackers can use a linux based tool called Yersinia. Yersinia allows an attacker to send DTP frames. It has many tools for layer 2 based network attacks.
- Scapy can be used for Double Tagging. A hacker can craft the doubel tagged frames in Python.
