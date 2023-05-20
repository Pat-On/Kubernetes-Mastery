# Rolling Update Walkthrough

## Rolling updates in practice

- as of kubernetes 1.8 we can do rolling updates with
  - `deployments`
  - `daemonsets`
  - `statefulsets`
- editing one of these resources will automatically result in a rolling update
- rolling updates can be monitored with `kubectl rollout` subcommand

## Rolling out the new `worker` service

exercise:
- lets monitor what is going on by opening a few terminals and run:
  - kubectl get pods -w
  - kubectl get replicasets -w
  - kubectl get deployments -w
- update `worker` either with `kubect edit` or by running:
  - kubectl set image deploy worker worker=dockercoins/worker:v0.2


## give it some time
- at first it looks like nothing is happening (the graph remains at the same level)
- according to `kubectl get deploy -w` the `deployment` was updated really quickly
- but `kubectl get pods -w` tells a different story
- the old `pods` are still here, and they stay in `Terminating` state for a while
- eventually they are terminated; and then the graph decreases significatnyl
- this delay is due to the fact that our worker does not handle signals
- kubernetes send a `polite` shutdown request to the worker, which ignore it
- after a grace period, Kubernetes get impatient and kills the container
  - the grace period is 30 seconds but can be changed if needed

## Rolling out something invalid
- what happens if we make a mistake
  
exercise:
- update `worker` by specifying a non-existing image:
- kubectl set image deploy worker worker=dockercoins/worker:v0.3
- chyeck what is going on:
  - kubectl rollout status deploy worker


Links:
https://kubernetes.io/docs/concepts/workloads/pods/#termination-of-pods