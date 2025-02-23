---
published: true
---
# **Planes: Control, Data, Management**

Sorry to dissapoint but we will not be discussing the engineering behind a Boeing 747 in this blog post. Instead we will be discussing the Control, Data and Management planes. A network device is typically divided into 3 seperate portions of operation. These three planes all have different features and affect how a router functions. Let's dive in and see what exactly are these network planes and their purpose.

## Control Plane

- The control plane's purpose is to determine the best pathway for a packet. Resources in the control plan handle the routing portion of a network device. Traffic from the control plane is sent to a router or originates from the router itself. The control plane is responsible for populating the routing table, which is used to populate the forwarding table. This means the data plane relies on the control plane to function. The control plain is known as the brain of the network due to this fact.

- Dynamic Routing Protocols (OSPF, BGP, ISIS etc), ICMP, ARP, DHCP, STP & LACP are some known control plane protocols.

- The control plane is software based and utilizes CPU rather than hardware like ASIC.


## Data Plane

- The data plane's purpose is to forward the actual packets/frames from one interface to another. Switching is what occurs in the data plane rather than routing. The data plane will direct input packets to an output interface all based on the control planes routing logic. It is also known as the forwarding plane because it is responsible for moving packets from source to destination. Think of a packet that is passing in transit on the network as data plane traffic.

- The forwarding table (FIB), process switching & CEF switching are all data plane protocols and procedures.

- The data plane is hardware based utilizing hardware tools like ASIC and needs to be fast and have low latency.

## Management Plane

- The management plane is traffic that used to manage/control the device on the network. The management protocols are typically used to monitor the device as well as for CLI access. The management plan is actually a subset of the control plane. This is because the destination of the traffic would be for the local device (ex. SSH to a router).

- SSH, SNMP, Telnet & FTP are examples of management plane protocols.