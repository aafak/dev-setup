# WSL (Windows Subsystem for Linux)
Allows you to run a Linux distribution alongside your Windows system without needing a separate virtual machine or dual boot.
Here’s how you can install and use WSL on Windows:

# Install WSL:  Open powershell and type following command
```
PS C:\Users\aafakmoh>  wsl --install
```
# Start WSL:
```
PS C:\Users\aafakmoh> wsl
Provisioning the new WSL instance Ubuntu
This might take a while...
Create a default Unix user account: aafak
New password: test
Retype new password: test
passwd: password updated successfully
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 5.15.167.4-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Mon Mar  3 04:21:52 UTC 2025

  System load:  0.0                 Processes:             32
  Usage of /:   0.1% of 1006.85GB   Users logged in:       0
  Memory usage: 5%                  IPv4 address for eth0: 192.168.57.27
  Swap usage:   0%

This message is shown once a day. To disable it please create the
/home/aafak/.hushlogin file.
aafak@windows:/mnt/c/Users/aafakmoh$
```

# From the window file explore type and hot enter: \\wsl$

# Change Memory setting for WSL:
https://learn.microsoft.com/en-us/windows/wsl/wsl-config

```
Check free memory in wsl:
aafak@windows:/mnt/c/Users/aafakmoh$ free -h
               total        used        free      shared  buff/cache   available
Mem:           7.6Gi       595Mi       6.9Gi       3.1Mi       283Mi       7.0Gi
Swap:          2.0Gi          0B       2.0Gi

Exit from WSL and open a file
aafak@windows:/mnt/c/Users/aafakmoh$ exit
logout
PS C:\Users\aafakmoh> notepad $env:USERPROFILE\.wslconfig
PS C:\Users\aafakmoh> cat $env:USERPROFILE\.wslconfig
[wsl2]
memory=10GB  # Set memory limit (e.g., 10GB)
processors=4  # Set number of CPU cores
swap=8GB  # Set swap file size

Shutdown
PS C:\Users\aafakmoh> wsl --shutdown
Restart and check
PS C:\Users\aafakmoh> wsl
aafak@HPE-5CG3360726:/mnt/c/Users/aafakmoh$ free -h
               total        used        free      shared  buff/cache   available
Mem:           9.7Gi       557Mi       9.1Gi       3.1Mi       275Mi       9.2Gi
Swap:          8.0Gi          0B       8.0Gi
aafak@HPE-5CG3360726:/mnt/c/Users/aafakmoh$
```

# WSL Dynamically Adjusting Memory Usage
By default, WSL2 does not have a fixed memory allocation. Instead, it dynamically adjusts its memory usage based on the workload and available system resources.
This means: If your WSL2 instance needs more RAM, it will request it from Windows. If WSL2 no longer needs memory, it will gradually release it back to Windows.

There's no predefined limit on how much memory WSL2 can use unless manually restricted. What Happens When You Restrict Memory Using .wslconfig?
When you set a memory limit in .wslconfig, WSL2 will be forced to stay within that limit, preventing it from consuming all available RAM.

[wsl2]
memory=4GB
WSL2 can use up to 4GB, but not more. Even if more RAM is available in Windows, WSL2 will not exceed 4GB. This prevents WSL2 from competing with other Windows applications for memory.

# Why Restrict Memory in WSL2?
 - Prevent Windows from Slowing Down
 - If WSL2 consumes too much memory, Windows applications might struggle.
 - Control Performance for Development
 - If you run multiple services in WSL2, setting a memory cap prevents one process from hogging all resources.
 - Better Stability in Heavy Workloads
 - Limiting memory can help prevent system crashes or unresponsiveness.
