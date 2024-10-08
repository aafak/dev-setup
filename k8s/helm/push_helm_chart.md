# Create helm chart

```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ ls
cmd  Dockerfile  go.mod  go.sum  helm  internal  Jenkinsfile  LICENSE  Makefile  README.md

aafak@aafak-virtual-machine:~/go_apps/auth-service$ ls helm/
Chart.yaml  dev-values.yaml  templates  values-prod.yaml  values.yaml
aafak@aafak-virtual-machine:~/go_apps/auth-service$

aafak@aafak-virtual-machine:~/go_apps/auth-service$ helm package ./helm/
Successfully packaged chart and saved it to: /home/aafak/go_apps/auth-service/auth-service-0.0.0.tgz

aafak@aafak-virtual-machine:~/go_apps/auth-service$ ls
auth-service-0.0.0.tgz  cmd  Dockerfile  go.mod  go.sum  helm  internal  Jenkinsfile  LICENSE  Makefile  README.md
aafak@aafak-virtual-machine:~/go_apps/auth-service$
```
# Push helm chart

```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ helm registry login docker.io/aafak/auth-service:0.0.0
Username: aafak
Password:
Login Succeeded
aafak@aafak-virtual-machine:~/go_apps/auth-service$

aafak@aafak-virtual-machine:~/go_apps/auth-service$ export HELM_EXPERIMENTAL_OCI=1

aafak@aafak-virtual-machine:~/go_apps/auth-service$ helm push auth-service-0.0.0.tgz oci://docker.io/aafak
Pushed: docker.io/aafak/auth-service:0.0.0
Digest: sha256:14a985e66a12970361a7504c88beaebb181858ec4ae8471419b50b0f6ca809a5
aafak@aafak-virtual-machine:~/go_apps/auth-service$

```

# Now you can see in docker hub

![image](https://github.com/user-attachments/assets/19d323e7-e278-4549-a00f-f17d10a83de9)

# Pull the helm chart in another system
```

aafak@aafak-virtual-machine:~/go_apps/auth-service$helm registry login docker.io
Username: aafak
Password:
Login Succeeded
aafak@aafak-virtual-machine:~/go_apps/auth-service$
aafak@aafak-virtual-machine:~/go_apps/auth-service$ helm pull oci://docker.io/aafak/auth-service --version 0.0.0

Pulled: docker.io/aafak/auth-service:0.0.0
Digest: sha256:14a985e66a12970361a7504c88beaebb181858ec4ae8471419b50b0f6ca809a5
aafak@aafak-virtual-machine:~/go_apps/auth-service$
aafak@aafak-virtual-machine:~/go_apps/auth-service$
```

# Install the chart
```
helm install my-release oci://docker.io/aafak/auth-service --version 0.0.0

``
