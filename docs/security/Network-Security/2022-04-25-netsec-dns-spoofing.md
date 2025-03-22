# **DNS Spoofing**

Todays topic DNS spoofing! I hope you all enjoy this one.

## What is DNS Spoofing?

A Distributed Denial of Service (DDoS) attack is a malicious network attack whose goal is to stop or interrupt an online application or service by overloading it's system. DDoS attacks are calculated and usualy come from multiple compromised hosts called a Bot Army. Each device is used to flood a service with a specific type of traffic. DDoS attacks can be split into 3 different category types:

### Volume Based Attacks
- This attacks goal is to saturate the bandwidth of an attacked site.
- UDP Floods, ICMP Floods and spoof-based attackeds are Volume attacks.
- Measured in Bps (Bits per second)

###  Protocol Attacks
 - Protocol based attacks aim to consume up a victims resources.
 - SYN Flood, Ping of Death, Smurf DDoS are Protocol Attacks.
 - Measured in Pps (Packets per second)

### Application Layer Attacks
 - Application Layer attacks aim to crash the web server
 - GET/POST Floods and typically attack Nginx, Apache, Windows, Linux based vulenerabilities.
 - Measuered in Rps (Requests per second)

## Types of DDoS Attacks

### UDP Flood
- Floods a target with UDP packets on random ports on a host. This forces the host constantly check the application for the connection and when it doesnt find an active session it will respond with an ICMP ‘Destination Unreachable’ packet. This drains the resources of the target host.
    
### SYN Flood
- Floods a target with TCP SYN requests packets. This causes the host to respond with a SYN-ACK packet. The target ends ups waiting forever for an ACK from the attacker causing resources to be tied up until no new connections can be made.

### HTTP Flood
 - Floods a target with GET or POST HTTP requests. These look legit so it is hard for a target host to determine what is legit or not. The goal is take utilize the resources on a host.

### ICMP Flood
- Overwhelms a target with ICMP Echo Request (ping) packets. The target host will attempt to reply to the attacker with ICMP Reply packets causing exhaustion of bandwidth and internal resources.

### Ping of Death (POD)
- The max size of an IP packet is 65,535 bytes. The data-link layer typically has a max frame size of 1500 bytes. This means a large IP packet has to be broken down into multiple fragments and then reassembled by the target host. If a host attempts to reassemble a packet larger than 65,535 bytes mememory buffer overflow errors can occur.

### Slowloris
- Allows a single computer to take down a webhost. Slowloris works by opening multiple connections to a web server and keeping them open as long as possible. Slowloris sends multiple HTTP headers for each request and never looks to complete the request. Eventually the connection pool on a host is filled and the target host can no longer accept new connections. Slowloris as the name states is meant to be a slow working attack.

### NTP Amplification
- An attacker will exploit a public NTP server and overhelm a victim host with UDP traffic. The amplification is due the fact that a compromised NTP host can easily send a very high amount of UDP traffic resulting in a high bandwidth & high volume attack.

### Smurf DDoS
- An attacker spoofs an IP address and sends an ICMP request to a victim. The victim will send a ICMP reply to which the attacker will echo the response back to the victim. This creates an infinite loop and eventually crashes the system.

## Mitigation Techniques

There are many ways to mitigate a DDoS attack. Even more than listed here. I believe a good combination of a few in conjuction will help round out your networks defense to a DDoS attack.

### Anycast Network
- Anycast allows different servers to share the same IP address. BGP allows hosts to find the best route to the nearest anycast address. Anycast networks allows network traffic to be spread out. A DDoS attack would have to take down every server in the anycast network.

### Firewall & Network Monitoring
- Configure firewall to protect against flood attacks. Monitor traffic so you can keep traffic of patterns and determine when an attack is possible.

### Cloud Multi Region Hosted Application
- Have an application configured to work in different physical regions this way the blast radius would be large for a DDoS attack.

### Utilize BGP with an ISP
 - Work with an ISP to route traffic away when a DDoS attack is detected.

### Upstream filtering
-  Cloudflare or Amazon Shield work by checking incoming packet IPs against known attackers and BotNets and attempt to only forward legitimate traffic.
- Stops the attack before it reaches your network.

### CDN Network
- Avoids a single point of congestion by having multiple PoPs.
- Distributes content across the globe or regions.

### Anti DDoS Systems
-  Arbor Networks, Akamai, CloudFlare, Radware