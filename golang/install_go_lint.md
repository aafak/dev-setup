
# Install go lint:
https://golangci-lint.run/

```
aafak@aafak-virtual-machine:~/go_install$ curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.59.1
golangci/golangci-lint info checking GitHub for tag 'v1.59.1'
golangci/golangci-lint info found version: 1.59.1 for v1.59.1/linux/amd64
golangci/golangci-lint info installed /home/aafak/go/bin/golangci-lint
aafak@aafak-virtual-machine:~/go_install$

aafak@aafak-virtual-machine:~$ ls $(go env GOPATH)/bin/golangci-lint
/home/aafak/go/bin/golangci-lint
aafak@aafak-virtual-machine:~$ export PATH=$PATH:$(go env GOPATH)/bin
aafak@aafak-virtual-machine:~$ which golangci-lint
/home/aafak/go/bin/golangci-lint
aafak@aafak-virtual-machine:~$ golangci-lint --version
golangci-lint has version 1.59.1 built with go1.22.3 from 1a55854a on 2024-06-09T18:08:33Z
aafak@aafak-virtual-machine:~$
aafak@aafak-virtual-machine:~/go_install$ source ~/.profile

export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$(go env GOPATH)/bin
aafak@aafak-virtual-machine:~$ source ~/.profile
aafak@aafak-virtual-machine:~$ which golangci-lint
/home/aafak/go/bin/golangci-lint
aafak@aafak-virtual-machine:~$  golangci-lint --version
golangci-lint has version 1.59.1 built with go1.22.3 from 1a55854a on 2024-06-09T18:08:33Z
aafak@aafak-virtual-machine:~$
aafak@aafak-virtual-machine:~/Private-Cloud/dsc-onprem-seed$ golangci-lint cache clean
aafak@aafak-virtual-machine:~/Private-Cloud/dsc-onprem-seed$
aafak@aafak-virtual-machine:~/Private-Cloud/dsc-onprem-seed$ golangci-lint run
```

# Test golint
```
aafak@aafak-virtual-machine:~/go_install$ mkdir gotest
aafak@aafak-virtual-machine:~/go_install$ cd gotest/
aafak@aafak-virtual-machine:~/go_install/gotest$ go mod init gotest
go: creating new go.mod: module gotest
go: to add module requirements and sums:
        go mod tidy
aafak@aafak-virtual-machine:~/go_install/gotest$ go mod tidy
aafak@aafak-virtual-machine:~/go_install/gotest$ ls
go.mod  test.go
aafak@aafak-virtual-machine:~/go_install/gotest$ golangci-lint run
test.go:1: : # gotest
./test.go:4:3: undefined: fmt (typecheck)
package main
aafak@aafak-virtual-machine:~/go_install/gotest$ cat test.go
package main

func main(){
  fmt.Println("Hello GO")
}
aafak@aafak-virtual-machine:~/go_install/gotest$
aafak@aafak-virtual-machine:~/go_install/gotest$ golangci-lint -j 2 run --timeout 30m
aafak@aafak-virtual-machine:~/go_install/gotest$ golangci-lint cache clean
```
