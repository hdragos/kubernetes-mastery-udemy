### Assignment 2

####1. Create a deployment called littletomcat using the tomcat image.

Create the deployment using the following command:
`kubectl create deployment littletomcat --image=tomcat`

####2. What command will help you get the IP address of that Tomcat server?

List all pods with their details using the following command:
`kubectl get pods --selector=app=littletomcat -o wide`

Describe individual pods using the following command:
`kubectl describe pod littletomcat-ABC-XYZ`

####3. What steps would you take to ping it from another container?

Open another terminal with shpod and run a ping command.

####4. What command would delete the running pod inside that deployment?

Delete all of the pods of our app using the following command:
`kubectl delete pods --selector=app=littletomcat`

####5. What happens if we delete the pod while the ping command is running?

If we delete the pod, the following things will happen:

* Kubernetes will gracefully terminate the pod

* Because the pod is no longer available, the IP address is no longer valid, so the ping command fails

* The replica set will kick in and see that it doesn't have enough active pods, so it will create a new one

* The newly created pod will have a different IP address, that means the ping command still won't work

####6. What command can give our Tomcat server a stable DNS name and IP address?

We need to create a service with ClusterIP for our deployment by running the following command:
`kubectl create service clusterip littletomcat --tcp 8080`

####7. What commands would you run to curl Tomcat with that DNS address?

Make a request to the littletomcat service

`curl http://littletomcat:8080`

If in shpod, you need to specify the different namespace

`curl http://littletomcat.default:8080`

Note that shpod runs in the shpod namespace, so to find a DNS name of a different namespace in the same cluster, you should use `<hostname>.<namespace>` syntax. That was a little advanced, so A+ if you got it on the first try!

Also Note, shpod is set so that kubectl uses the default namespace as its context, which means you don't have to add -n default to all your kubectl commands.

####8. If we delete the pod that holds Tomcat, does the IP address still work? How could we test that?

Yes. Deleting the pod will not affect the ClusterIP. However, there may be a short period while there are no pods active
so that could cause the curl to fail.