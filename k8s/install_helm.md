# Install helm in ubunutu

```
sudo apt-get update

sudo apt-get install apt-transport-https ca-certificates -y

curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -

sudo apt-get install software-properties-common
sudo add-apt-repository "deb https://baltocdn.com/helm/stable/debian/ all main"

sudo apt-get update
sudo apt-get install helm

```

# Check version
```
aafak@aafak-virtual-machine:~$ helm version
version.BuildInfo{Version:"v3.16.1", GitCommit:"5a5449dc42be07001fd5771d56429132984ab3ab", GitTreeState:"clean", GoVersion:"go1.22.7"}
aafak@aafak-virtual-machine:~$

```
