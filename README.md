# k8s-lamp
Kubernetes files to install LAMP Stack

## Build MYSQL

Change the folder to mysql.
### Use this command to create a secret password
```
kubectl create secret generic mysql-pass --from-file=password.txt
```
### Create a deploy and service for mysql server.
```
kubectl apply -f mysql.yaml
```
### Check those service and pod 
```
kubectl get pod
NAME                              READY     STATUS    RESTARTS   AGE
php-server-2153209126-5dq92       1/1       Running   0          2d

kubectl get svc
NAME               CLUSTER-IP       EXTERNAL-IP    PORT(S)    AGE
mysql-service      192.171.74.152   <none>         3306/TCP   2d
```
## Build PHP
change the folder to php.
### Create a deploy and service for php server.
```
kubectl apply -f php.yaml
```