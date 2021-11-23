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
mysql-server-688d5669f5-jxgrl       1/1       Running   0          2d

kubectl get svc
NAME               CLUSTER-IP       EXTERNAL-IP    PORT(S)    AGE
mysql-service      192.171.74.152   <none>         3306/TCP   2d
```
## Build Apache and PHP
change the folder to php.

### Create a deploy and persistenVolume for PHP and Apache Server.
```
kubectl apply -f persistentVolume.yaml
```
### Create a deploy and service for php server.
```
kubectl apply -f php.yaml
```

### Create a deploy and service for Apache server.
```
kubectl apply -f apache.yaml
```

### Check Pods
```
kubectl get pods
```

```
NAME                                READY   STATUS    RESTARTS   AGE
apache-deployment-bf56458db-zglnb   1/1     Running   0          13m
my-php7-server-5857b6cc59-n8h8q     1/1     Running   0          14m
mysql-server-688d5669f5-jxgrl       1/1     Running   0          17m
```

### Test Shared PersistentVolume Apache and PHP

Go to inside the PHP Pod to write a file on /data
```
kubectl exec -it my-php7-server-5857b6cc59-n8h8q /bin/sh
cd /data
touch test.txt
```

Go to inside the Apache Pod to check the written file.
```
kubectl exec -it apache-deployment-bf56458db-zglnb /bin/bash
> var/www/html # cd /data
> /data # ls
> test.txt
```

## Elasticsearch

Install Helm
```
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

Using helm to install Elasticsearch

Add Helm repository
```
helm repo add elastic https://helm.elastic.co
```

Install Elasticsearch with helm
```
helm install elasticsearch elastic/elasticsearch
```
