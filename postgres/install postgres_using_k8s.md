# Install postgres

**Create a deployment file:**

```
aafak@aafak-virtual-machine:~$ vim postgres-deployment.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: postgres-pv
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data/postgres"

---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:13
        ports:
        - containerPort: 5433  # Set the container port to 5433
        env:
        - name: POSTGRES_USER
          value: "aafak"
        - name: POSTGRES_PASSWORD
          value: "test"
        - name: POSTGRES_DB
          value: "authz"
        - name: PGPORT              # Set the PostgreSQL port to 5433
          value: "5433"
        volumeMounts:
        - mountPath: /var/lib/postgresql/data
          name: postgres-storage
      volumes:
      - name: postgres-storage
        persistentVolumeClaim:
          claimName: postgres-pvc

---

apiVersion: v1
kind: Service
metadata:
  name: postgres
spec:
  selector:
    app: postgres
  ports:
    - protocol: TCP
      port: 5433             # Service port to access PostgreSQL
      targetPort: 5433       # Target port should also match the container port
  type: NodePort             # Use NodePort to allow external access
```

# Install
```
aafak@aafak-virtual-machine:~$ kubectl apply -f postgres-deployment.yaml
persistentvolume/postgres-pv created
persistentvolumeclaim/postgres-pvc created
deployment.apps/postgres created
service/postgres created
```

# Verify deployment
```
aafak@aafak-virtual-machine:~$ kubectl get pods
NAME                         READY   STATUS    RESTARTS       AGE
nginx-web-5b757f798d-ftd98   1/1     Running   6 (110m ago)   224d
postgres-d74f49844-h922g     1/1     Running   0              7s
todo-app-5f64775dbb-l2mnf    1/1     Running   0              104m
todo-app-5f64775dbb-l8rc6    1/1     Running   0              103m
todo-app-5f64775dbb-lzz7v    1/1     Running   0              103m
aafak@aafak-virtual-machine:~$ kubectl logs -f postgres-d74f49844-h922g

PostgreSQL Database directory appears to contain a database; Skipping initialization

2024-09-22 12:46:49.524 UTC [1] LOG:  starting PostgreSQL 13.16 (Debian 13.16-1.pgdg120+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 12.2.0-14) 12.2.0, 64-bit
2024-09-22 12:46:49.525 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5433
2024-09-22 12:46:49.525 UTC [1] LOG:  listening on IPv6 address "::", port 5433
2024-09-22 12:46:49.527 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5433"
2024-09-22 12:46:49.536 UTC [26] LOG:  database system was shut down at 2024-09-22 12:46:00 UTC
2024-09-22 12:46:49.547 UTC [1] LOG:  database system is ready to accept connections


aafak@aafak-virtual-machine:~$ kubectl get svc
NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes     ClusterIP   10.96.0.1       <none>        443/TCP          224d
nginx-web      NodePort    10.109.6.236    <none>        80:31755/TCP     224d
postgres       NodePort    10.102.100.59   <none>        5433:30623/TCP   74s
todo-service   NodePort    10.96.94.48     <none>        80:31000/TCP     21d
aafak@aafak-virtual-machine:~$

aafak@aafak-virtual-machine:~$ minikube ip
192.168.49.2
aafak@aafak-virtual-machine:~$


aafak@aafak-virtual-machine:~$ psql -h 192.168.49.2 -p 30623 -U aafak -d authz
Password for user aafak:
psql (14.13 (Ubuntu 14.13-0ubuntu0.22.04.1), server 13.16 (Debian 13.16-1.pgdg120+1))
Type "help" for help.

authz=#


```
