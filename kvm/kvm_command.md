virsh and virt-* are two types of command-line tools commonly used to manage virtual machines with KVM (Kernel-based Virtual Machine) and libvirt. While they are related, they serve different purposes and have distinct use cases. Here's a breakdown of their differences:

**1. virsh: The Domain Manager**
Primary Purpose: virsh is a command-line interface used to manage virtual machine domains directly through the libvirt API.

**Use Cases:**
Starting, stopping, and managing VMs.
Creating and managing storage volumes and pools.
Handling networks and interfaces.
Viewing and modifying VM configurations.

**Examples:**

**Start a VM:** virsh start my-vm
**Undefine (delete) a VM:** virsh undefine my-vm
**List all active VMs:** virsh list

**Advantages:**
Direct interaction with the libvirt API.
Granular control over VM resources like disks, networks, and interfaces.
Scripting-friendly for automation.

**2. virt-*: Higher-Level Utility Tools**
Primary Purpose: The virt-* suite (e.g., virt-install, virt-clone, virt-manager) is a collection of tools designed to simplify specific tasks related to virtual machine management. These tools often wrap around libvirt functionality.

**Key Tools:**
**virt-install:** Create and configure new VMs.
**virt-clone**: Clone existing VMs.
**virt-manager:** GUI-based VM management.
**virt-sysprep:** Prepare a VM image for cloning or redistribution.
**virt-viewer:** View VM consoles graphically.

Examples:

**Create a VM:** virt-install --name my-vm --ram 2048 --vcpus 2 --disk size=20 --os-variant ubuntu20.04 --graphics none
**Clone a VM:**  virt-clone --original my-vm --name my-vm-clone --file /path/to/disk.img

**Advantages:**
Task-specific tools streamline common operations like creating or cloning VMs.
Better suited for users who prefer simpler, higher-level commands.
Often provide additional features for specific tasks (e.g., OS installation automation in virt-install).

```
root@aafak:~# virsh pool-list
 Name    State    Autostart
-----------------------------
 local   active   yes

root@aafak:~# virsh vol-create-as local aafak-vm1-disk.qcow2 1G --format qcow2
Vol aafak-vm1-disk.qcow2 created

root@aafak:~# virsh vol-list local
 Name                   Path
--------------------------------------------------------------------
 aafak-vm1-disk.qcow2   /var/kvm/vms/aafak-vm1-disk.qcow2

root@aafak:~#

root@aafak:~# virsh net-list
 Name         State    Autostart   Persistent
-----------------------------------------------
 Management   active   yes         yes

root@aafak:~#

root@aafak:~# virt-install --name aafak-vm1 --ram 512 --vcpus 1 --disk path=/var/kvm/vms/aafak-vm1-disk.qcow2,format=qcow2 --os-type linux --os-variant generic --network network=Management --graphics none --boot hd --noautoconsole
WARNING  --os-type is deprecated and does nothing. Please stop using it.
WARNING  Using --osinfo generic, VM performance may suffer. Specify an accurate OS for optimal results.

Starting install...
Creating domain...                                                                                        |    0 B  00:00:00
Domain creation completed.
root@aafak:~#
root@aafak:~# virsh list
 Id   Name        State
---------------------------
 4    aafak-vm1   running

root@aafak:~#
root@aafak:~# virsh destroy aafak-vm1 && virsh undefine aafak-vm1 --remove-all-storage
Domain 'aafak-vm1' destroyed

Domain 'aafak-vm1' has been undefined
Volume 'hda'(/var/kvm/vms/aafak-vm1-disk.qcow2) removed.

root@aafak:~# virsh list
 Id   Name   State
--------------------

root@aafak:~#
root@aafak:~# virsh list
 Id   Name        State
---------------------------
 5    aafak-vm1   running

root@aafak:~#  virsh destroy aafak-vm1 && virsh undefine aafak-vm1 --remove-all-storage
Domain 'aafak-vm1' destroyed

Domain 'aafak-vm1' has been undefined
Volume 'hda'(/var/kvm/vms/aafak-vm1-disk.qcow2) removed.

root@aafak:~# virsh list --all
 Id   Name   State
--------------------

root@aafak:~#
root@aafak:~# virsh destroy aafak-vm1 && virsh undefine aafak-vm1 --remove-all-storage
error: failed to get domain 'aafak-vm1'

root@aafak:~#

root@mvm-host-2--dns-servers10:~# virsh list
 Id   Name        State
---------------------------
 7    aafak-vm1   running

root@mvm-host-2--dns-servers10:~# virsh shutdown aafak-vm1
Domain 'aafak-vm1' is being shutdown

```
