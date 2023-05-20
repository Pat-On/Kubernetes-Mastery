# Rolling Update

- By default (without rolling updates), when a scaled resource is updated:
  - new pods are created
  - old pods are terminated
  - ... all at the same time
  - if something goes wrong. mess
  - it is day to day operation 
  - (all done before this chapter was day one)

- with rolling updates, when a Deployment is updated, it happens progressively
- the deployment control multiple ReplicaSets
- each ReplicaSet is a group of identical Pods
  - with the same image, arguments, parameters...
- during the rolling update, we have at least two ReplicaSets
  - the `new` set (corresponding to the `target` version)
  - at least one `old` set

- We can have multiple old sets
  - if we start another update before the first one is done

## Update Strategy
- two parameters determine the pace of the rollout: `maxUnavailable` and `maxSurge`
- they can be specified in absolute number of pods or percentage of the `replicas` count
- at any given time...
  - there will always be at least `replicas-maxUnavailable` pods available
  - there will never be more than `replicas` + `maxSurge` pods in total
  - there will therefore be up to `maxUnavailable` + `maxSurge` pods being updated

- We have  the possibility of rolling back to the previous version
  - if the update fail or is unsatisfactory in any way

## checking current rollout parameters
- recall how we build custom reports with `kubectl` and `jq`:
  
exercise:
- show the rollout plan for out deployments:

`kubectl get deploy -o json | jq ".items[] | {name:.metadata.name} + .spec.strategy.rollingUpdate"`

Links:
https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/
https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/