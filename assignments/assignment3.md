### Assignment 3: Wordsmith

#### 1. Create the deployments for each microservice

```shell
kubectl create deployment web --image=bretfisher/wordsmith-web
kubectl create deployment words --image=bretfisher/wordsmith-words
kubectl create deployment db --image=bretfisher/wordsmith-db
```

Note: the images use hardcoded names of other images. So if you create a deployment `wordsmith-words`
for the image `bretfisher/wordsmith-words`, the web image won't work, as it expects a service
named `words`, not `wordsmith-words`.

#### 2. Expose the services

```shell
kubectl expose deployment/words --port=8080
kubectl expose deployment/db --port=5432
kubectl expose deployment/web --type=NodePort --port=80
```

#### 3. Scale up the words service
```shell
kubectl scale deployment/wordsmith-words --replicas=5
```

#### 4. Cleanup

```shell
kubectl delete svc/words
kubectl delete svc/db
kubectl delete svc/web
kubectl delete deployment/words
kubectl delete deployment/db
kubectl delete deployment/web
```