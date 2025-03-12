# Install Docker:
 - https://docs.docker.com/engine/install/ubuntu/#install-from-a-package

```
aafak@aafak-virtual-machine:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
docker: Error response from daemon: Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers).
See 'docker run --help'.
aafak@aafak-virtual-machine:~$
```

# Set the Proxy:
```
aafak@aafak-virtual-machine:~$ sudo mkdir -p /etc/systemd/system/docker.service.d
aafak@aafak-virtual-machine:~$ sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf
[Service]
Environment="HTTP_PROXY=http://proxy.its.corp.net:8080"
Environment="HTTPS_PROXY=http://proxy.its.corp.net:8080"
aafak@aafak-virtual-machine:~$
```

# Update Private registry:
```
aafak@aafak-virtual-machine:~/python311/Python-3.11.0$ cat /etc/docker/daemon.json
{
"insecure-registries": ["aafak.corp.net:443", "aafak-harbor.in.corp.net"],
"exec-opts": ["native.cgroupdriver=systemd"]
}
```

# Flush changes and restart Docker
```
 sudo systemctl daemon-reload
 sudo systemctl restart docker
 
 aafak@aafak-virtual-machine:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete
Digest: sha256:88ec0acaa3ec199d3b7eaf73588f4518c25f9d34f58ce9a0df68429c5af48e8d
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

aafak@aafak-virtual-machine:~$
```

