# Install Go in Ubuntu:
https://go.dev/dl/

```
aafak@aafak-virtual-machine:~/go_install$ curl -OL https://go.dev/dl/go1.20.linux-amd64.tar.gz
aafak@aafak-virtual-machine:~/go_install$ sudo tar -C /usr/local -xvf go1.20.linux-amd64.tar.gz
aafak@aafak-virtual-machine:~/go_install$ sudo vim ~/.profile
export PATH=$PATH:/usr/local/go/bin
aafak@aafak-virtual-machine:~/go_install$ source ~/.profile
aafak@aafak-virtual-machine:~/go_install$ go version
go version go1.20 linux/amd64
```
