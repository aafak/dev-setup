# Install argo cd in minikube cluster
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
