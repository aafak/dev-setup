# Install Docker:
 - https://docs.docker.com/engine/install/ubuntu/#install-from-a-package
```
aafak@aafak-vm:~/install_docker$ curl -fsSL https://get.docker.com -o get-docker.sh
aafak@aafak-vm:~/install_docker$ ls
get-docker.sh
aafak@aafak-vm:~/install_docker$ sudo sh get-docker.sh
# Executing docker install script, commit: 4c94a56999e10efcf48c5b8e3f6afea464f9108e
+ sh -c apt-get -qq update >/dev/null
+ sh -c DEBIAN_FRONTEND=noninteractive apt-get -y -qq install ca-certificates curl >/dev/null
+ sh -c install -m 0755 -d /etc/apt/keyrings
+ sh -c curl -fsSL "https://download.docker.com/linux/ubuntu/gpg" -o /etc/apt/keyrings/docker.asc

curl: (28) Failed to connect to download.docker.com port 443 after 300291 ms: Timeout was reached
aafak@aafak-vm:~/install_docker$
```

- If not worked from packaged install manually
```
aafak@aafak-vm:~/install_docker$ sudo mkdir -p /etc/apt/keyrings
aafak@aafak-vm:~/install_docker$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
aafak@aafak-vm:~/install_docker$ echo "deb [signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
aafak@aafak-vm:~/install_docker$
aafak@aafak-vm:~/install_docker$ sudo apt update
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease
Hit:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease
Get:4 https://download.docker.com/linux/ubuntu noble InRelease [48.8 kB]
Hit:5 http://archive.ubuntu.com/ubuntu noble-backports InRelease
Get:6 https://download.docker.com/linux/ubuntu noble/stable amd64 Packages [20.3 kB]
Fetched 69.2 kB in 3s (27.2 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
9 packages can be upgraded. Run 'apt list --upgradable' to see them.
aafak@aafak-vm:~/install_docker$ sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  docker-ce-rootless-extras git git-man liberror-perl libslirp0 pigz slirp4netns
Suggested packages:
  cgroupfs-mount | cgroup-lite git-daemon-run | git-daemon-sysvinit git-doc git-email git-gui gitk gitweb git-cvs
  git-mediawiki git-svn
The following NEW packages will be installed:
  containerd.io docker-buildx-plugin docker-ce docker-ce-cli docker-ce-rootless-extras docker-compose-plugin git git-man
  liberror-perl libslirp0 pigz slirp4netns
0 upgraded, 12 newly installed, 0 to remove and 9 not upgraded.
Need to get 125 MB of archives.
After this operation, 462 MB of additional disk space will be used.
Get:1 https://download.docker.com/linux/ubuntu noble/stable amd64 containerd.io amd64 1.7.25-1 [29.6 MB]
Get:2 http://archive.ubuntu.com/ubuntu noble/universe amd64 pigz amd64 2.8-1 [65.6 kB]
Get:3 http://archive.ubuntu.com/ubuntu noble/main amd64 liberror-perl all 0.17029-2 [25.6 kB]
Get:4 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 git-man all 1:2.43.0-1ubuntu7.2 [1,100 kB]
....
.....
Setting up docker-ce-rootless-extras (5:28.0.1-1~ubuntu.24.04~noble) ...
Setting up slirp4netns (1.2.1-1build2) ...
Setting up docker-ce (5:28.0.1-1~ubuntu.24.04~noble) ...
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /usr/lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /usr/lib/systemd/system/docker.socket.
Setting up git (1:2.43.0-1ubuntu7.2) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for libc-bin (2.39-0ubuntu8.4) ...

aafak@aafak-vm:~/install_docker$ docker --version
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
Docker version 28.0.1, build 068a01e
Synchronizing state of docker.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Wed 2025-03-12 17:07:22 IST; 11s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 18869 (dockerd)
      Tasks: 10
     Memory: 20.7M (peak: 21.4M)
        CPU: 1.242s
     CGroup: /system.slice/docker.service
             └─18869 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Mar 12 17:07:21 aafak-vm dockerd[18869]: time="2025-03-12T17:07:21.007556464+05:30" level=info msg="OTEL tracing is not configu>
Mar 12 17:07:21 aafak-vm dockerd[18869]: time="2025-03-12T17:07:21.007918039+05:30" level=info msg="detected 127.0.0.53 nameser>
Mar 12 17:07:21 aafak-vm dockerd[18869]: time="2025-03-12T17:07:21.209995191+05:30" level=info msg="Loading containers: start."
Mar 12 17:07:22 aafak-vm dockerd[18869]: time="2025-03-12T17:07:22.718167263+05:30" level=info msg="Loading containers: done."
Mar 12 17:07:22 aafak-vm dockerd[18869]: time="2025-03-12T17:07:22.773779658+05:30" level=info msg="Docker daemon" commit=bbd0a>
Mar 12 17:07:22 aafak-vm dockerd[18869]: time="2025-03-12T17:07:22.774104394+05:30" level=info msg="Initializing buildkit"
Mar 12 17:07:22 aafak-vm dockerd[18869]: time="2025-03-12T17:07:22.873992099+05:30" level=info msg="Completed buildkit initiali>
Mar 12 17:07:22 aafak-vm dockerd[18869]: time="2025-03-12T17:07:22.889082204+05:30" level=info msg="Daemon has completed initia>
Mar 12 17:07:22 aafak-vm dockerd[18869]: time="2025-03-12T17:07:22.889214941+05:30" level=info msg="API listen on /run/docker.s>
Mar 12 17:07:22 aafak-vm systemd[1]: Started docker.service - Docker Application Container Engine.
lines 1-22/22 (END)

aafak@aafak-vm:~/install_docker$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
aafak@aafak-vm:~/install_docker$ sudo docker pull hello-world
Using default tag: latest
Error response from daemon: Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers)
aafak@aafak-vm:~/install_docker$

aafak@aafak-vm:~/install_docker$ sudo mkdir -p /etc/systemd/system/docker.service.d
aafak@aafak-vm:~/install_docker$ sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf
aafak@aafak-vm:~/install_docker$ sudo systemctl daemon-reload
aafak@aafak-vm:~/install_docker$ sudo systemctl restart docker
aafak@aafak-vm:~/install_docker$ sudo docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
e6590344b1a5: Pull complete
Digest: sha256:bfbb0cc14f13f9ed1ae86abc2b9f11181dc50d779807ed3a3c5e55a6936dbdd5
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
aafak@aafak-vm:~/install_docker$

```

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

