# Install postgres using helm

First install Helm and then install postgres

# Add helm repo
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

```

# Create a values.yaml
```
aafak@aafak-virtual-machine:~$ vim values.yaml

postgresqlUsername: aafak
postgresqlPassword: test
postgresqlDatabase: authz

service:
  port: 5433  # Change this to your desired port
postgresqlPort: 5433  # Change this to your desired port

persistence:
  enabled: true
  size: 10Gi
```

# Install
```
aafak@aafak-virtual-machine:~$ helm install postgresql bitnami/postgresql -f values.yaml
NAME: postgresql
LAST DEPLOYED: Sun Sep 22 16:42:00 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: postgresql
CHART VERSION: 15.5.32
APP VERSION: 16.4.0

** Please be patient while the chart is being deployed **

PostgreSQL can be accessed via port 5432 on the following DNS names from within your cluster:

    postgresql.default.svc.cluster.local - Read/Write connection

To get the password for "postgres" run:

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace default postgresql -o jsonpath="{.data.postgres-password}" | base64 -d)

To connect to your database run the following command:

    kubectl run postgresql-client --rm --tty -i --restart='Never' --namespace default --image docker.io/bitnami/postgresql:16.4.0-debian-12-r9 --env="PGPASSWORD=$POSTGRES_PASSWORD" \
      --command -- psql --host postgresql -U postgres -d postgres -p 5432

    > NOTE: If you access the container using bash, make sure that you execute "/opt/bitnami/scripts/postgresql/entrypoint.sh /bin/bash" in order to avoid the error "psql: local user with ID 1001} does not exist"

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace default svc/postgresql 5432:5432 &
    PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432

WARNING: The configured password will be ignored on new installation in case when previous PostgreSQL release was deleted through the helm command. In that case, old PVC will have an old password, and setting it through helm won't take effect. Deleting persistent volumes (PVs) will solve the issue.

WARNING: There are "resources" sections in the chart not set. Using "resourcesPreset" is not recommended for production. For production installations, please set the following values according to your workload needs:
  - primary.resources
  - readReplicas.resources
+info https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
aafak@aafak-virtual-machine:~$
```

# Verify
```

aafak@aafak-virtual-machine:~$ helm list
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
postgresql      default         1               2024-09-22 17:25:57.330951975 +0530 IST deployed        postgresql-15.5.32      16.4.0
aafak@aafak-virtual-machine:~$ kubectl get svc
NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.96.0.1      <none>        443/TCP        224d
nginx-web       NodePort    10.109.6.236   <none>        80:31755/TCP   224d
postgresql      ClusterIP   10.98.254.9    <none>        5432/TCP       93s
postgresql-hl   ClusterIP   None           <none>        5432/TCP       93s
todo-service    NodePort    10.96.94.48    <none>        80:31000/TCP   21d
aafak@aafak-virtual-machine:~$ kubectl get pods
NAME                         READY   STATUS    RESTARTS      AGE
nginx-web-5b757f798d-ftd98   1/1     Running   6 (60m ago)   224d
postgresql-0                 1/1     Running   0             98s
todo-app-5f64775dbb-l2mnf    1/1     Running   0             55m
todo-app-5f64775dbb-l8rc6    1/1     Running   0             54m
todo-app-5f64775dbb-lzz7v    1/1     Running   0             54m
aafak@aafak-virtual-machine:~$


```
