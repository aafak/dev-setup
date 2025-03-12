# Install Ubuntu:

From the wired setting, Update IP, gateway, dsn, proxy

Ubuntu: apt install proxy settings
 sudo vim /etc/apt/apt.conf.d/proxy.conf
 
 Acquire {
    HTTP::proxy "http://proxy.its.corp.net:8080";
    HTTPS::proxy "http://proxy.its.corp.net:8080";
}

Run:
  sudo apt-get update

Enable ssh:
 https://linuxhint.com/enable-use-ssh-ubuntu/
 sudo apt install openssh-server -y


Now try ssh:
