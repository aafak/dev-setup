# Create Helm chart

```
aafak@aafak-virtual-machine:~/go_apps/auth-service$ ls
cmd  Dockerfile  go.mod  go.sum  helm  internal  Jenkinsfile  LICENSE  Makefile  README.md
aafak@aafak-virtual-machine:~/go_apps/auth-service$ ls helm/
Chart.yaml  templates  values-prod.yaml  values.yaml
aafak@aafak-virtual-machine:~/go_apps/auth-service$

aafak@aafak-virtual-machine:~/go_apps/auth-service$ helm install  auth-service ./helm -f ./helm/values.yaml
NAME: auth-service
LAST DEPLOYED: Tue Oct  8 12:52:15 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None


aafak@aafak-virtual-machine:~/go_apps/auth-service$ kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
auth-service-56dd954cfb-lghhw   1/1     Running   0          48s
postgres-7768954946-7bl85       1/1     Running   0          14d
aafak@aafak-virtual-machine:~/go_apps/auth-service$ kubectl get svc
NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
auth-service   ClusterIP   10.98.104.53    <none>        8080/TCP         54s
kubernetes     ClusterIP   10.96.0.1       <none>        443/TCP          15d
postgres       NodePort    10.96.153.222   <none>        5433:32738/TCP   14d
aafak@aafak-virtual-machine:~/go_apps/auth-service$ kubectl get deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
auth-service   1/1     1            1           60s
postgres       1/1     1            1           14d
aafak@aafak-virtual-machine:~/go_apps/auth-service$


aafak@aafak-virtual-machine:~/go_apps/auth-service$ kubectl exec -it auth-service-56dd954cfb-lghhw -- sh
~ # env
KUBERNETES_PORT=tcp://10.96.0.1:443
KUBERNETES_SERVICE_PORT=443
LOG_LEVEL=info
DEBUG_MODE=false
DATABASE_URL=postgresql://localhost:5432/mydb
HOSTNAME=auth-service-56dd954cfb-lghhw
DB_PORT=5433
AUTH_SERVICE_PORT_8080_TCP_ADDR=10.98.104.53
AUTH_SERVICE_SERVICE_HOST=10.98.104.53
SHLVL=1
HOME=/root
DB_NAME=authz
AUTH_SERVICE_PORT_8080_TCP_PORT=8080
CONFIG_JSON={
  "version": "1.0",
  "settings": {
    "theme": "light",
    "max_retries": 3
  }
}

AUTH_SERVICE_PORT_8080_TCP_PROTO=tcp
AUTH_SERVICE_SERVICE_PORT=8080
AUTH_SERVICE_PORT=tcp://10.98.104.53:8080
AUTH_SERVICE_PORT_8080_TCP=tcp://10.98.104.53:8080
TERM=xterm
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
KUBERNETES_PORT_443_TCP_PORT=443
POSTGRES_PORT_5433_TCP_ADDR=10.96.153.222
KUBERNETES_PORT_443_TCP_PROTO=tcp
POSTGRES_SERVICE_HOST=10.96.153.222
POSTGRES_PORT_5433_TCP_PORT=5433
POSTGRES_URL=postgresql://localhost:5432/mydb
POSTGRES_PORT_5433_TCP_PROTO=tcp
POSTGRES_PORT=tcp://10.96.153.222:5433
POSTGRES_SERVICE_PORT=5433
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
APP_ENV=production
DB_PASSWORD=test
POSTGRES_SERVICE_NAME=postgres
KUBERNETES_SERVICE_HOST=10.96.0.1
PWD=/root
AUTH_SERVICE_SERVICE_PORT_REST=8080
POSTGRES_PORT_5433_TCP=tcp://10.96.153.222:5433
DB_HOST=postgres
DB_USER=aafak
~ #

```
