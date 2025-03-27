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
