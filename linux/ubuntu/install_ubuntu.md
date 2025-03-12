# Install Ubuntu:
From the wired setting, Update IP, gateway, dsn, proxy

Ubuntu: apt install proxy settings
sudo vim /etc/apt/apt.conf.d/proxy.conf
``` 
 Acquire {
    HTTP::proxy "http://proxy.its.corp.net:8080";
    HTTPS::proxy "http://proxy.its.corp.net:8080";
}
```

# Update packages:
```
aafak@aafak-vm:~$ sudo apt-get update
```

# Enable ssh:
 -  https://linuxhint.com/enable-use-ssh-ubuntu/

```
aafak@aafak-vm:~$  sudo apt install openssh-server -y
```

# Install curl
```
aafak@aafak-vm:~$ sudo apt install curl
```

# Set proxy permanently
```
aafak@aafak-vm:~/install_docker$ sudo vim ~/.bashrc

Add following line at the end:

export http_proxy=http://proxy.its.corp.net:8080
export https_proxy=http://proxy.its.corp.net:8080
export HTTP_PROXY=http://proxy.its.corp.net:8080
export HTTPS_PROXY=http://proxy.its.corp.net:8080

aafak@aafak-vm:~/install_docker$ source ~/.bashrc
aafak@aafak-vm:~/install_docker$ curl -fsSL https://get.docker.com -o get-docker.sh
aafak@aafak-vm:~/install_docker$ ls
get-docker.sh

```

Now try ssh:
