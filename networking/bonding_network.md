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

**Mode 4 (802.3ad):** Uses LACP (Link Aggregation Control Protocol) for dynamic link aggregation.

**Mode 5 (balance-tlb):** Adaptive transmit load balancing.

**Mode 6 (balance-alb):** Adaptive load balancing, for both transmit and receive load balancing.

# Netplan
In Ubuntu and other Linux distributions that use Netplan for network configuration, you can define a bonded network interface like bond0 by editing the Netplan configuration files located in** /etc/netplan/**. Here's a step-by-step guide to configuring network bonding with Netplan.

**1. Create or Edit the Netplan Configuration File:**
Netplan configuration files are usually located in /etc/netplan/. The files are in YAML format and typically have a .yaml extension. You can either create a new one or modify an existing one (e.g., 00-netcfg.yaml).

**2. Example Netplan Configuration for bond0:**
Below is an example of how to define a bond0 interface in a Netplan configuration file, bonding two physical interfaces eth0 and eth1 in active-backup mode (i.e., one is active, and the other is on standby in case the active one fails):

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

# Explanation of the Fields:
**version: 2**: Specifies the version of the Netplan YAML format.

**renderer:** networkd: Specifies that systemd-networkd is the network backend to use. You could use NetworkManager instead if you are in a desktop environment.

**ethernets:** Defines the physical Ethernet interfaces (eth0 and eth1). Here, we disable dhcp4 for these interfaces since they will be bonded into bond0.

**bonds:** Defines the bond0 interface.
**dhcp4: yes:** Configures the bond to use DHCP to get an IP address.
**interfaces:** Lists the physical interfaces to be bonded (in this case, eth0 and eth1).
**parameters:**
mode: active-backup: Sets the bonding mode to active-backup, where one interface is active, and the other is on standby for failover.
**primary: eth0:** Specifies that eth0 is the primary interface to be used.
mii-monitor-interval: 100: Sets the monitoring interval to check the availability of the links (100 ms).

**addresses:** 192.168.1.100/24: This assigns a static IP (192.168.1.100) with a subnet mask of /24 (255.255.255.0). 

**gateway4:** 192.168.1.1: Specifies the gateway for the bond.

**nameservers:** addresses: Specifies the DNS servers (in this case, Google DNS servers 8.8.8.8 and 8.8.4.4).

**interfaces:** eth0 and eth1 are the bonded interfaces.

**parameters:** The bond mode is active-backup with a 100 ms monitoring interval for checking interface health.

# Exp2
```
admin@hv-ubuntu:~$ cat /etc/netplan/netplan1.yaml
network:
  version: 2
  renderer: networkd
  bonds:
    bond0:
      interfaces:
        - ens192
      parameters:
        mode: active-backup
      dhcp4: false
      addresses:
        - 172.25.81.17/16
      routes:
        - to: default
          via: 172.25.17.2
      nameservers:
        addresses: [16.100.155.51,16.100.155.52]
      link-local: [ipv4,ipv6]
  ethernets:
    ens192:
      dhcp4: false
	  
```
# Apply
```	 
$ sudo netplan generate
$ sudo netplan apply
```
# Verifying the Bonding and IP Assignment
```
ip addr show bond0

cat /proc/net/bonding/bond0
```
