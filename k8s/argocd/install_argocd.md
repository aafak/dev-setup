# Install argo cd in minikube cluster
https://www.youtube.com/watch?v=ZgJQG475oME&list=PLdpzxOOAlwvKu7OZpgj1-MzJFqZ8RBp6f&index=3

https://argo-cd.readthedocs.io/en/stable/getting_started/

```
aafak@aafak-virtual-machine:~$ kubectl get nodes
NAME       STATUS   ROLES           AGE    VERSION
minikube   Ready    control-plane   101m   v1.28.3
aafak@aafak-virtual-machine:~$

aafak@aafak-virtual-machine:~$ kubectl create namespace argocd
namespace/argocd created
aafak@aafak-virtual-machine:~$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
customresourcedefinition.apiextensions.k8s.io/applications.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/applicationsets.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/appprojects.argoproj.io created
serviceaccount/argocd-application-controller created
serviceaccount/argocd-applicationset-controller created
serviceaccount/argocd-dex-server created
serviceaccount/argocd-notifications-controller created
serviceaccount/argocd-redis created
serviceaccount/argocd-repo-server created
serviceaccount/argocd-server created
role.rbac.authorization.k8s.io/argocd-application-controller created
role.rbac.authorization.k8s.io/argocd-applicationset-controller created
role.rbac.authorization.k8s.io/argocd-dex-server created
role.rbac.authorization.k8s.io/argocd-notifications-controller created
role.rbac.authorization.k8s.io/argocd-redis created
role.rbac.authorization.k8s.io/argocd-server created
clusterrole.rbac.authorization.k8s.io/argocd-application-controller created
clusterrole.rbac.authorization.k8s.io/argocd-applicationset-controller created
clusterrole.rbac.authorization.k8s.io/argocd-server created
rolebinding.rbac.authorization.k8s.io/argocd-application-controller created
rolebinding.rbac.authorization.k8s.io/argocd-applicationset-controller created
rolebinding.rbac.authorization.k8s.io/argocd-dex-server created
rolebinding.rbac.authorization.k8s.io/argocd-notifications-controller created
rolebinding.rbac.authorization.k8s.io/argocd-redis created
rolebinding.rbac.authorization.k8s.io/argocd-server created
clusterrolebinding.rbac.authorization.k8s.io/argocd-application-controller created
clusterrolebinding.rbac.authorization.k8s.io/argocd-applicationset-controller created
clusterrolebinding.rbac.authorization.k8s.io/argocd-server created
configmap/argocd-cm created
configmap/argocd-cmd-params-cm created
configmap/argocd-gpg-keys-cm created
configmap/argocd-notifications-cm created
configmap/argocd-rbac-cm created
configmap/argocd-ssh-known-hosts-cm created
configmap/argocd-tls-certs-cm created
secret/argocd-notifications-secret created
secret/argocd-secret created
service/argocd-applicationset-controller created
service/argocd-dex-server created
service/argocd-metrics created
service/argocd-notifications-controller-metrics created
service/argocd-redis created
service/argocd-repo-server created
service/argocd-server created
service/argocd-server-metrics created
deployment.apps/argocd-applicationset-controller created
deployment.apps/argocd-dex-server created
deployment.apps/argocd-notifications-controller created
deployment.apps/argocd-redis created
deployment.apps/argocd-repo-server created
deployment.apps/argocd-server created
statefulset.apps/argocd-application-controller created
networkpolicy.networking.k8s.io/argocd-application-controller-network-policy created
networkpolicy.networking.k8s.io/argocd-applicationset-controller-network-policy created
networkpolicy.networking.k8s.io/argocd-dex-server-network-policy created
networkpolicy.networking.k8s.io/argocd-notifications-controller-network-policy created
networkpolicy.networking.k8s.io/argocd-redis-network-policy created
networkpolicy.networking.k8s.io/argocd-repo-server-network-policy created
networkpolicy.networking.k8s.io/argocd-server-network-policy created
aafak@aafak-virtual-machine:~$

```
# Verify the installation

```
aafak@aafak-virtual-machine:~$ kubectl get pods -n argocd
NAME                                                READY   STATUS    RESTARTS   AGE
argocd-application-controller-0                     1/1     Running   0          117s
argocd-applicationset-controller-6dfb7b585b-s556d   1/1     Running   0          119s
argocd-dex-server-69cdf4f66-85zvb                   1/1     Running   0          119s
argocd-notifications-controller-768c89485f-j22qx    1/1     Running   0          119s
argocd-redis-686d6f888b-nthq2                       1/1     Running   0          119s
argocd-repo-server-54dc76d497-j5dkv                 1/1     Running   0          119s
argocd-server-8c67b6d56-rkrnn                       1/1     Running   0          118s
aafak@aafak-virtual-machine:~$ kubectl get deployments -n argocd
NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
argocd-applicationset-controller   1/1     1            1           2m5s
argocd-dex-server                  1/1     1            1           2m5s
argocd-notifications-controller    1/1     1            1           2m5s
argocd-redis                       1/1     1            1           2m5s
argocd-repo-server                 1/1     1            1           2m5s
argocd-server                      1/1     1            1           2m5s
aafak@aafak-virtual-machine:~$ kubectl get svc -n argocd
NAME                                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
argocd-applicationset-controller          ClusterIP   10.105.19.154   <none>        7000/TCP,8080/TCP            2m11s
argocd-dex-server                         ClusterIP   10.107.58.3     <none>        5556/TCP,5557/TCP,5558/TCP   2m11s
argocd-metrics                            ClusterIP   10.103.125.9    <none>        8082/TCP                     2m11s
argocd-notifications-controller-metrics   ClusterIP   10.99.44.226    <none>        9001/TCP                     2m11s
argocd-redis                              ClusterIP   10.109.4.167    <none>        6379/TCP                     2m11s
argocd-repo-server                        ClusterIP   10.101.36.92    <none>        8081/TCP,8084/TCP            2m11s
argocd-server                             ClusterIP   10.103.215.90   <none>        80/TCP,443/TCP               2m10s
argocd-server-metrics                     ClusterIP   10.97.2.234     <none>        8083/TCP                     2m10s
aafak@aafak-virtual-machine:~$
```

# Access the ArgoCD
Edit the argocd-server service type NodePort
```
aafak@aafak-virtual-machine:~$ kubectl edit svc argocd-server -n argocd
service/argocd-server edited
aafak@aafak-virtual-machine:~$ kubectl get svc -n argocd
NAME                                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
argocd-applicationset-controller          ClusterIP   10.105.19.154   <none>        7000/TCP,8080/TCP            5m22s
argocd-dex-server                         ClusterIP   10.107.58.3     <none>        5556/TCP,5557/TCP,5558/TCP   5m22s
argocd-metrics                            ClusterIP   10.103.125.9    <none>        8082/TCP                     5m22s
argocd-notifications-controller-metrics   ClusterIP   10.99.44.226    <none>        9001/TCP                     5m22s
argocd-redis                              ClusterIP   10.109.4.167    <none>        6379/TCP                     5m22s
argocd-repo-server                        ClusterIP   10.101.36.92    <none>        8081/TCP,8084/TCP            5m22s
argocd-server                             NodePort    10.103.215.90   <none>        80:31245/TCP,443:31851/TCP   5m21s
argocd-server-metrics                     ClusterIP   10.97.2.234     <none>        8083/TCP                     5m21s
aafak@aafak-virtual-machine:~$

aafak@aafak-virtual-machine:~$ minikube service list -n argocd
|-----------|-----------------------------------------|--------------|---------------------------|
| NAMESPACE |                  NAME                   | TARGET PORT  |            URL            |
|-----------|-----------------------------------------|--------------|---------------------------|
| argocd    | argocd-applicationset-controller        | No node port |                           |
| argocd    | argocd-dex-server                       | No node port |                           |
| argocd    | argocd-metrics                          | No node port |                           |
| argocd    | argocd-notifications-controller-metrics | No node port |                           |
| argocd    | argocd-redis                            | No node port |                           |
| argocd    | argocd-repo-server                      | No node port |                           |
| argocd    | argocd-server                           | http/80      | http://192.168.49.2:31245 |
|           |                                         | https/443    | http://192.168.49.2:31851 |
| argocd    | argocd-server-metrics                   | No node port |                           |
|-----------|-----------------------------------------|--------------|---------------------------|
aafak@aafak-virtual-machine:~$ minikube service argocd-server -n argocd
|-----------|---------------|-------------|---------------------------|
| NAMESPACE |     NAME      | TARGET PORT |            URL            |
|-----------|---------------|-------------|---------------------------|
| argocd    | argocd-server | http/80     | http://192.168.49.2:31245 |
|           |               | https/443   | http://192.168.49.2:31851 |
|-----------|---------------|-------------|---------------------------|
[argocd argocd-server http/80
https/443 http://192.168.49.2:31245
http://192.168.49.2:31851]
aafak@aafak-virtual-machine:~$
With in the same ubuntu VM, you can access it using the above IP
```
Browse the https://192.168.49.2:31245/
![image](https://github.com/user-attachments/assets/0bd56e6b-da59-4aea-bb68-5f034440b2e0)

# Access from Laptop using the VM IP with port formwarding
```
aafak@aafak-virtual-machine:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:33:78:23 brd ff:ff:ff:ff:ff:ff
    altname enp2s1
    inet **192.168.203.128/24** brd 192.168.203.255 scope global dynamic noprefixroute ens33
       valid_lft 1053sec preferred_lft 1053sec
    inet6 fe80::690a:a290:9d86:f7c2/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: br-3ebe9952fd2c: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:8d:aa:d6:d8 brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global br-3ebe9952fd2c
       valid_lft forever preferred_lft forever
4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:6e:82:06:94 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:6eff:fe82:694/64 scope link
       valid_lft forever preferred_lft forever
5: br-d631a5a76bf7: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:35:d6:3a:8b brd ff:ff:ff:ff:ff:ff
    inet 192.168.49.1/24 brd 192.168.49.255 scope global br-d631a5a76bf7
       valid_lft forever preferred_lft forever
    inet6 fe80::42:35ff:fed6:3a8b/64 scope link
       valid_lft forever preferred_lft forever
7: veth9fb5cc3@if6: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-d631a5a76bf7 state UP group default
    link/ether 0e:1f:23:12:ad:23 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::c1f:23ff:fe12:ad23/64 scope link
       valid_lft forever preferred_lft forever
aafak@aafak-virtual-machine:~$

aafak@aafak-virtual-machine:~$ kubectl port-forward svc/argocd-server -n argocd 9001:80 --address=0.0.0.0
Forwarding from 0.0.0.0:9001 -> 8080
Handling connection for 9001
Handling connection for 9001
Handling connection for 9001
Handling connection for 9001
````

Browse from the laptop usng VM IP: https://192.168.203.128:9001/

![image](https://github.com/user-attachments/assets/089c8464-3408-477f-b1a2-ffc7567d9725)


# Get the default argocd password
```
aafak@aafak-virtual-machine:~$ kubectl get secrets -n argocd
NAME                          TYPE     DATA   AGE
argocd-initial-admin-secret   Opaque   1      19m
argocd-notifications-secret   Opaque   0      20m
argocd-redis                  Opaque   1      19m
argocd-secret                 Opaque   5      20m
aafak@aafak-virtual-machine:~$ kubectl edit  secret argocd-initial-admin-secret -n argocd
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: v1
data:
  password: TERzUHlPZUVyT3BkSEVGYw==
kind: Secret
metadata:
  creationTimestamp: "2025-02-26T05:52:50Z"
  name: argocd-initial-admin-secret
  namespace: argocd
  resourceVersion: "5369"
  uid: 19faf7e4-a3e7-4ff6-8332-a73cca7adf87
type: Opaque

aafak@aafak-virtual-machine:~$ echo TERzUHlPZUVyT3BkSEVGYw== | base64 --decode
LDsPyOeErOpdHEFc
aafak@aafak-virtual-machine:~$
You can login with admin/LDsPyOeErOpdHEFc
```

![image](https://github.com/user-attachments/assets/1962063d-27f8-420c-97f5-244636f4262a)

# Explore the example apps
https://github.com/argoproj/argocd-example-apps
https://github.com/argoproj/argocd-example-apps/tree/master/guestbook
https://github.com/argoproj/argocd-example-apps/tree/master/helm-guestbook

# Create the first app
![image](https://github.com/user-attachments/assets/5a88247d-f599-44c6-93d0-75968e75a458)


Click on create, you can see  will start syncing from gitrepo
![image](https://github.com/user-attachments/assets/b80a0865-6400-4073-ac10-30be1da43478)

![image](https://github.com/user-attachments/assets/e180fa21-4192-404d-9ded-2581b4be9419)


![image](https://github.com/user-attachments/assets/14288086-3a94-4677-8238-a6aca5c00ee6)

# Now verify the deployment: It has deplyed the application from the git repos(pods, service and deployment)

![image](https://github.com/user-attachments/assets/30c9a01f-c016-4461-beb9-ff86415bccae)




