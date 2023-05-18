# Interacting with Kubernetes

- we will interact with out Kubernetes cluster through the Kubernetes API
- The kubernetes API is mostly RESTful
- it allows us to create, read, update, delete resources
- a few common resource types are:
  - node (a machine - physical or virtual - in our cluster)
  - pod (group of containers running together on a node)
  - service (stable network endpoint to connect to one or multiple containers)

Pod
- abstract around containers
- lowest deployable unit


pod example:
IP-address
Containers logger + nginx (dockers)

## Pods
- pods are a new abstraction
- a pod can have multiple containers working together
- (but you usually only have one container per pod)
- pod is our smallest deployable unit; Kubernetes can not manage containers directly
- IP addresses are associated with pods, not with individual containers
- containers in a pod share localhost, and can share volumes
- multiple containers in a pod are deployed together
- in reality, Docker does not know a pod, only containers/namespaces/volumes

https://kubernetes.io/docs/concepts/workloads/pods/