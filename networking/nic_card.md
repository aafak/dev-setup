# Network Interface Card (NIC)
A Network Interface Card (NIC) is a hardware component that allows a device (like a computer or server) to connect to a network.
Each NIC typically has a unique identifier called a MAC address.

# Ethernet
Ethernet is a common networking technology used for local area networks (LANs).
It defines protocols for how data packets are formatted and transmitted over wired connections.
When you refer to an Ethernet interface (like eth0), you’re typically talking about a NIC that
uses Ethernet technology to communicate on a network.

if a Network Interface Card (NIC) has two ports, it typically has two separate MAC addresses—one for each port.
Here’s a bit more detail:

**Individual MAC Addresses:** Each port on a NIC operates independently and has its own MAC address.
This is essential for network communication, as MAC addresses uniquely identify devices on the same local network.

**Dual-Port NIC:** A dual-port NIC can be used for various purposes, such as redundancy (failover) or load balancing.
Each port can be connected to a different network segment, allowing for increased bandwidth and reliability.
Configuration:

In operating systems, these ports are usually represented as separate interfaces (e.g., eth0 and eth1 or enp3s0f0 and enp3s0f1). Each interface will have its own settings, including an IP address and MAC address.

**Use Cases:**

Dual-port NICs are common in servers, data centers, and high-performance computing environments where multiple network connections are needed for better performance, redundancy, or isolation of network traffic.
Example
If you have a dual-port NIC, the two MAC addresses might look something like this:

**Port 1 (e.g., eth0): MAC Address 00:11:22:33:44:55
Port 2 (e.g., eth1): MAC Address 00:11:22:33:44:56**
