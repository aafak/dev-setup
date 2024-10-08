# Install helm

```
aafak@aafak-virtual-machine:~$ curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 11694  100 11694    0     0   8425      0  0:00:01  0:00:01 --:--:--  8425
Downloading https://get.helm.sh/helm-v3.16.1-linux-amd64.tar.gz
Verifying checksum... Done.
Preparing to install helm into /usr/local/bin
[sudo] password for aafak:
helm installed into /usr/local/bin/helm
aafak@aafak-virtual-machine:~$ helm version
version.BuildInfo{Version:"v3.16.1", GitCommit:"5a5449dc42be07001fd5771d56429132984ab3ab", GitTreeState:"clean", GoVersion:"go1.22.7"}
aafak@aafak-virtual-machine:~$

```
