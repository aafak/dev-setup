# Setup private registry
Edit the file:
```
aafak@aafak-virtual-machine$ vim /etc/docker/daemon.json
{
"insecure-registries": ["reg1.corp.net:443", "reg2.corp.net", "reg3-cds.com"],
"exec-opts": ["native.cgroupdriver=systemd"]
}
```

# Flush changes and restart Docker
```
 sudo systemctl daemon-reload
 sudo systemctl restart docker
```
# Login to private registry
```
aafak@aafak-virtual-machine:~$ sudo docker login reg3-cds.com
[sudo] password for aafak:
Username: aafakm
Password: ******
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
aafak@aafak-virtual-machine:~$
```

# Pull from private registry
```
sudo docker pull reg3-cds.com/devops/ubuntu-atlas:22.04
```
