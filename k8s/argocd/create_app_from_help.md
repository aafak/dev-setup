# Create am App in the argoCD using the helm to deploy the auth service 
Deploy the service from the https://github.com/aafak/auth-service
![image](https://github.com/user-attachments/assets/1e1c5763-f617-4082-b29c-bd52cbb9ae98)

![image](https://github.com/user-attachments/assets/9614b1a5-e80b-40c9-8465-e5ea31913f1c)

![image](https://github.com/user-attachments/assets/baeb88a5-0d8a-4c12-a2a2-05a375970111)


![image](https://github.com/user-attachments/assets/6b567a7e-10e1-4d72-b922-d2a19f2a5e1f)

![image](https://github.com/user-attachments/assets/9240c660-97e2-4edc-bff4-b5c58060bdba)


# Now verify the deployment
```
aafak@aafak-virtual-machine:~$ kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
auth-service-f9c59d66b-k4vbg   1/1     Running   0          114s
postgres-d74f49844-kbb4s       1/1     Running   0          143m
aafak@aafak-virtual-machine:~$ kubectl get svc
NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
auth-service   ClusterIP   10.98.121.143   <none>        8080/TCP         2m
kubernetes     ClusterIP   10.96.0.1       <none>        443/TCP          159m
postgres       NodePort    10.97.167.219   <none>        5433:31052/TCP   143m
aafak@aafak-virtual-machine:~$ kubectl get deployment
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
auth-service   1/1     1            1           2m7s
postgres       1/1     1            1           143m
aafak@aafak-virtual-machine:~$

```











