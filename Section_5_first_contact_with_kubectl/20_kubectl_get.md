# more `get` commands: services

- A service is a stable endpoint to connect to something
  (in the initial proposal, they were called portals) 

exercise:
- list the services on our cluster with one of these commands:
  - `kubectl get services`
  - `kubectl get svc`


# listing running containers
- containers are manipulated through pods
- a pod is a group of containers
  - running together (on the same node)
  - sharing resources (RAM, CPU, but also network, volumes)

exercise:
- list pods on our cluster : `kubectl get pods`
                    something like `docker ps` `docker container ls`


https://kubernetes.io/docs/reference/kubectl/#operations