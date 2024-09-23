# Create Docker file
```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ ls
cmd  Dockerfile  go.mod  go.sum  internal  Jenkinsfile  LICENSE  Makefile  README.md
aafak@aafak-virtual-machine:~/go_apps/auth-service$

aafak@aafak-virtual-machine:~/go_apps/auth-service$ Vim Dockerfile
# Dockerfile
FROM golang:1.20-alpine AS builder
ARG PROXY
# Set environment variables for the proxy
ENV http_proxy=${PROXY}
ENV https_proxy=${PROXY}
ENV no_proxy=localhost,127.0.0.1

# install build tools
RUN set -eux; \
    apk add -U --no-cache \
        curl \
        git  \
        make \
        bash \
    ;

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN ls
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ./cmd/

FROM alpine:latest

# RUN apk --no-cache add ca-certificates

WORKDIR /root/

COPY --from=builder /app/main .
# COPY --from=builder /app/.env .

EXPOSE 8080

CMD ["./main"]
```

# Build Image
```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ sudo docker build --build-arg PROXY=http://proxy.corp.net:8080 -t aafak/auth-service:latest .
[+] Building 93.1s (17/17) FINISHED                                                                              docker:default
 => [internal] load .dockerignore                                                                                          0.0s
 => => transferring context: 2B                                                                                            0.0s
 => [internal] load build definition from Dockerfile                                                                       0.0s
 => => transferring dockerfile: 721B                                                                                       0.0s
 => [internal] load metadata for docker.io/library/alpine:latest                                                           0.0s
 => [internal] load metadata for docker.io/library/golang:1.20-alpine                                                      0.0s
 => CACHED [builder 1/8] FROM docker.io/library/golang:1.20-alpine                                                         0.0s
 => CACHED [stage-1 1/3] FROM docker.io/library/alpine:latest                                                              0.0s
 => [internal] load build context                                                                                          0.1s
 => => transferring context: 3.81kB                                                                                        0.0s
 => [builder 2/8] RUN set -eux;     apk add -U --no-cache         curl         git          make         bash     ;       13.5s
 => [stage-1 2/3] WORKDIR /root/                                                                                           0.2s
 => [builder 3/8] WORKDIR /app                                                                                             0.1s
 => [builder 4/8] COPY go.mod go.sum ./                                                                                    0.2s
 => [builder 5/8] RUN go mod download                                                                                     42.6s
 => [builder 6/8] COPY . .                                                                                                 0.3s
 => [builder 7/8] RUN ls                                                                                                   0.7s
 => [builder 8/8] RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ./cmd/                              34.5s
 => [stage-1 3/3] COPY --from=builder /app/main .                                                                          0.3s
 => exporting to image                                                                                                     0.4s
 => => exporting layers                                                                                                    0.3s
 => => writing image sha256:c4fe1c4cb368af277a4f1529130154545e077fc668ba5e27bac7505416c14c32                               0.0s
 => => naming to docker.io/aafak/auth-service:latest           
```

# login to docker
```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ sudo docker images | grep aafak
aafak/auth-service            latest              c4fe1c4cb368   6 minutes ago   30.4MB

aafak@aafak-virtual-machine:~/go_apps/auth-service$ docker login
Log in with your Docker ID or email address to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com/ to create one.
You can log in with your password or a Personal Access Token (PAT). Using a limited-scope PAT grants better security and is required for organizations using SSO. Learn more at https://docs.docker.com/go/access-tokens/

Username: aafak
Password:
WARNING! Your password will be stored unencrypted in /home/aafak/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```
# Push the image
```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ docker push aafak/auth-service:latest
The push refers to repository [docker.io/aafak/auth-service]
c10164b15753: Pushed
5f70bf18a086: Mounted from library/golang
63ca1fbb43ae: Mounted from library/alpine
latest: digest: sha256:3b832f70ae6a1a02cd7aabc33d6c74263b4f909d98c07885b477d346c987833d size: 946
aafak@aafak-virtual-machine:~/go_apps/auth-service$

```
