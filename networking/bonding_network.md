# Network bonding
Network bonding is a method of combining multiple physical network interfaces into a single logical interface for redundancy, increased bandwidth, or load balancing. Here's a detailed explanation:

**1. Definition:**
bond0 is the name of the first logical network interface created when multiple physical network interfaces are bonded together.
The term bonding is used interchangeably with link aggregation or NIC teaming, depending on the operating system or configuration.
It’s primarily used in server environments to improve network performance and availability.

**2. Purpose of Network Bonding:**
Redundancy: If one network interface fails, the others continue to provide network connectivity, ensuring high availability.
Increased Bandwidth: By combining two or more network interfaces, you effectively increase the available bandwidth, as traffic can be balanced across the interfaces.
Load Balancing: Incoming and outgoing traffic can be distributed across the available network interfaces, optimizing the network load.

**3. How it Works:**
Multiple network interfaces (e.g., eth0, eth1, etc.) are bonded to form a logical interface (like bond0).
The bond0 interface inherits the IP address, routing, and network settings, while the physical interfaces (e.g., eth0, eth1) remain hidden.
Depending on the bonding mode, traffic is split or distributed between the physical interfaces.

**4. Bonding Modes:**
There are several bonding modes available, each serving different purposes:

**Mode 0 (balance-rr):** Round-robin load balancing (packets are sent sequentially across all interfaces).
**Mode 1 (active-backup):** One interface is active, and the others are backups (failover occurs when the active one fails).
**Mode 2 (balance-xor):** Transmissions are based on the source and destination MAC addresses.
**Mode 3 (broadcast):** All traffic is sent on all interfaces.
Mode 4 (802.3ad): Uses LACP (Link Aggregation Control Protocol) for dynamic link aggregation.
Mode 5 (balance-tlb): Adaptive transmit load balancing.
Mode 6 (balance-alb): Adaptive load balancing, for both transmit and receive load balancing.

# Example
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
    eth1:
      dhcp4: no
  bonds:
    bond0:
      interfaces:
        - eth0
        - eth1
      addresses:
        - 192.168.1.100/24  # Static IP and subnet
      gateway4: 192.168.1.1  # Gateway IP
      nameservers:
        addresses:
          - 8.8.8.8  # Google DNS
          - 8.8.4.4  # Google DNS
      parameters:
        mode: active-backup
        primary: eth0
        mii-monitor-interval: 100
```
