# Running our first containers on Kubernetes
- first things first: we cannot run a container
- We are going to run a pod, and in that pod there will be a single container
- in that container in the pod, we are going to run a simple `ping` command
- then we are going to start additional copies of the pod



## starting a simple pod with kubectl run

- we need to specify at least a name and the image we want to use
  
exercise: 
- lets ping `1.1.1.1` Cloudflate's public DNS resolver
  - `kubectl run pingpong --image alpine ping 1.1.1.1`

(Starting with Kubernetes 1.12 we get a message telling us that `kubectl run` is deprecated. Lets ignore it for now)


# behind the scenes of `kubectl run`
- lets look at the resource4s that were created by `kubectl run`

exercise:
- list most resource types:
  - `kubectl get all`

### behin the scenes of `kubectl run`
#### NOTE: starting in 1.18 run only creates a pod

```
pat@pat-GE62-2QF:~/Projects/kubernetes-mastery$ kubectl get all
NAME            READY   STATUS    RESTARTS   AGE
pod/pingpong2   1/1     Running   0          4m21s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   18h
```

OLD VERSION
```
Deployment (resource)
    ReplicaSet (resource)
        Pod(resource)
            Container (docker in our case)
                |ping 1.1.1.1
```


## What are these different things?
- a deployment is a high-level construct
  - allows scaling, rolling updates, rollbacks
  - multiple deployments can be used together to implement a canary deployment
  - delegates pods managemenet to replica sets

- A replica set is a low-level construct
  - make sure that a given number of identical pods are running
  - allows scaling
  - rarely used directly

- note: a replication controller is the (deprecated) predecessor of a replica set



Links:
https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#run
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
https://kubernetes.io/docs/reference/kubectl/docker-cli-to-kubectl/
https://kubernetes.io/docs/reference/kubectl/conventions/
