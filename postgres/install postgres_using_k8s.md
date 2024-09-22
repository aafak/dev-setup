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
        image: postgres:13    # Specify the PostgreSQL version
        ports:
        - containerPort: 5433
        env:
        - name: POSTGRES_USER       # Define the PostgreSQL user
          value: "aafak"
        - name: POSTGRES_PASSWORD   # Define the PostgreSQL password
          value: "test"
        - name: POSTGRES_DB         # Define the PostgreSQL database name
          value: "authz"
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
      port: 5433             # Port to access PostgreSQL
      targetPort: 5433
  type: ClusterIP            # Options: ClusterIP, NodePort, LoadBalancer
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
aafak@aafak-virtual-machine:~$ kubectl get svc
NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes     ClusterIP   10.96.0.1       <none>        443/TCP        224d
nginx-web      NodePort    10.109.6.236    <none>        80:31755/TCP   224d
postgres       ClusterIP   10.103.58.160   <none>        5433/TCP       8s
todo-service   NodePort    10.96.94.48     <none>        80:31000/TCP   21d
aafak@aafak-virtual-machine:~$ kubectl get pods
NAME                         READY   STATUS              RESTARTS      AGE
nginx-web-5b757f798d-ftd98   1/1     Running             6 (84m ago)   224d
postgres-6849448dd8-6rf4n    0/1     ContainerCreating   0             14s
todo-app-5f64775dbb-l2mnf    1/1     Running             0             78m
todo-app-5f64775dbb-l8rc6    1/1     Running             0             77m
todo-app-5f64775dbb-lzz7v    1/1     Running             0             77m
aafak@aafak-virtual-machine:~$ kubectl get pods
NAME                         READY   STATUS              RESTARTS      AGE
nginx-web-5b757f798d-ftd98   1/1     Running             6 (84m ago)   224d
postgres-6849448dd8-6rf4n    0/1     ContainerCreating   0             20s
todo-app-5f64775dbb-l2mnf    1/1     Running             0             78m
todo-app-5f64775dbb-l8rc6    1/1     Running             0             77m
todo-app-5f64775dbb-lzz7v    1/1     Running             0             77m
aafak@aafak-virtual-machine:~$ kubectl get pods
NAME                         READY   STATUS    RESTARTS      AGE
nginx-web-5b757f798d-ftd98   1/1     Running   6 (85m ago)   224d
postgres-6849448dd8-6rf4n    1/1     Running   0             2m3s
todo-app-5f64775dbb-l2mnf    1/1     Running   0             80m
todo-app-5f64775dbb-l8rc6    1/1     Running   0             79m
todo-app-5f64775dbb-lzz7v    1/1     Running   0             79m
aafak@aafak-virtual-machine:~$

```
