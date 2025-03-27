# WSL (Windows Subsystem for Linux)
Allows you to run a Linux distribution alongside your Windows system without needing a separate virtual machine or dual boot.
Here’s how you can install and use WSL on Windows:

# Install WSL:  Strat powershell and type following command
```
PS C:\Users\aafakmoh>  wsl --install
```
# Strat WSL:
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
aafak@HPE-5CG3360726:/mnt/c/Users/aafakmoh$
```

# From the window file explore type and hot enter: \\wsl$

# Change Memory setting for WSL:
https://learn.microsoft.com/en-us/windows/wsl/wsl-config

```
aafak@HPE-5CG3360726:/mnt/c/Users/aafakmoh$ sudo vim /etc/wsl.conf
[sudo] password for aafak:
aafak@HPE-5CG3360726:/mnt/c/Users/aafakmoh$ cat /etc/wsl.conf
[boot]
systemd=true

[user]
default=aafak

[automount]
options = "metadata,umask=22,fmask=11"

[wsl2]
# Limits VM memory to use no more than 4 GB
memory=10GB
# # Sets amount of swap storage space to 8GB
swap=8GB
```
aafak@HPE-5CG3360726:/mnt/c/Users/aafakmoh$
