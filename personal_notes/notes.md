## Base principles 

**Q: Why use Kubernetes? What problem does it solve?**

Kubernetes solves the problem of scaling. _**The problem with Docker (or any other container runtime for that matter)
is the fact that it is limited to one machine.**_ Containers are still an extremely powerful mechanism that helps with
deployment (their core strength is the common runtime and the fact that they can be easily packaged, distributed
and spun up). However, there is still a limited number of containers that a machine can run at the same time.

Since containers are a really powerful, yet limited tool used for application deployment, there is a need for _**a 
solution which can manage multiple containers on different machines**_. For this very purpose, Kubernetes was created.

**Q: What is Kubernetes?**

Kubernetes is a container manager (which can have multiple distributions) used for managing container clusters.
A really basic diagram about it can be found below:

![Kubernetes basic architecture diagram](./images/Kubernetes-architecture-diagram-1-1.png)

### Glossary

#### Control plane

One or more master nodes.

#### Docker 

The most popular container runtime for Kubernetes.

#### etcd

A key-value store used internally by Kubernetes, present on master nodes. 

#### Master node

A node that has several management processes running (like API server, Scheduler, Controller-Manager and etcd)

#### Node

Refers to a machine (physical or virtual) which can be used for various operations.

#### Pod

Pods are the abstraction over containers. They are not a binary or some other piece of code. They are merely
abstractions used by Kubernetes. A pod can contain one or more containers (most of the time a pod has only one 
container in it). _**Containers can never be interacted with directly.**_

_**IPs are associated with pods, not with containers.**_

All pods deployed on the same machine will share `localhost` and can also share volumes.

#### Worker / Worker Node

Refers to a worker node which has a container runtime and is able to run one or multiple pods.
