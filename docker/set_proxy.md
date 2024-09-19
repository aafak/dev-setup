# Setup proxy:

Edit the file:
```
aafak@aafak-virtual-machine:~$ sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf
[Service]
Environment="HTTP_PROXY=http://proxy.corp.net:8080"
Environment="HTTPS_PROXY=http://proxy.corp.net:8080"
```
# Flash the changes
```
aafak@aafak-virtual-machine:~$ sudo systemctl daemon-reload
aafak@aafak-virtual-machine:~$ sudo systemctl restart docker
```

# Test
```
aafak@aafak-virtual-machine:~$ sudo docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
```
