### Assignment 4: Load balancer

#### 1. Create, expose and connect to the NGINX instance

```shell
kubectl create deployment nginx --image=nginx
kubectl expose deployment/nginx --type=NodePort --port=80
kubectl get svc -l app=nginx
```

#### 2. Modify labels for the nginx service and deployment template

Edit the service config for nginx
```shell
kubectl edit service nginx
```
Look for:
```yaml
selector:
  app: nginx
```
and replace it with:
```yaml
selector:
  myapp: web
```

Trying to curl into nginx is no longer possible.

Edit the deployment config for nginx
```shell
kubectl edit deployment nginx
```

Look for:
```yaml
template:
  metadata:
    labels:
      app: nginx
```
and replace it with:
```yaml
template:
  metadata:
    labels:
      app: nginx
      myapp: web
```

This will affect how the deployment creates resources. The created resources will also have 
the labels `app: nginx` and `myapp: web`. 

#### 3. Create the Apache deployment and integrate it into the bootleg load balancer

```shell
kubectl create deployment apache --image=httpd
kubectl expose deployment/apache --type=NodePort --port=80
```

Modify the apache deployment the same way the nginx deployment was previously modified.

(Assuming that we are in a shpod) Run the following command:
```shell
curl http://nginx.default
```

It should return either an apache response or an nginx response (50/50 chance).

Bonus: scale up the apache deployment to 5 replicas.
```shell
kubectl scale deployment/apache --replicas=5
```

We will get more apache responses now, because our bootleg load balancer will have a higher chance to redirect to
apache pods.

#### Cleanup 

```shell
kubectl delete svc/nginx
kubectl delete deploy/apache
kubectl delete deploy/nginx
```