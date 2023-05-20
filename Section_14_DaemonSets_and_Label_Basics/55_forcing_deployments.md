# Forcing Deployment into DaemonSet

## Creating the YAML file for our daemon set
- lets start with the YAML file for the current `rng` resource

exercise:
- Dump the `rng` resource in YAML:"
  - `kubectl get deploy/rng -o yaml >rng.yml`

- edit `rng.yml`


## Understanding the problem
- the core of the error is:
  - error validating data <--- wrong things the schema

- obviously it does not make sense to specify a number of replicas for a daemon set
- workaround: fix the yaml
  - remote the `replicas` field
  - remove the `strategy` field (which defines the rollout mechanism for a deployment)
  - remote the `progressDeadlineSeconds` field (also used by the rollout mechanims)
  - remove the `status: {}` line at the end


## use the `--force`, Luke
- we could also tell kubernetes to ignore these errors and try anywah
- the `--force` flags actual name is `--validate=false`

Exercise 
try to load your YAML: file anmd ignore errors:
    `kubectl apply -f rng.yml --validate=false`


## Checking what we have done
- did we transform our `deployment` into a `daemonset`?
- look at the resource that we have now:
  - `kubectl get all`


# `deploy/rng` and `ds/rng`
- you can have different resource types with the same name
  - (ie a deployment and a daemon set both named`rng`)
- we still have the old `rng` deployment

deployment.apps/rng         1/1     1            1           6h23m


- but now we have the new `rng` daemon set as well
  
NAME                 DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/rng   1         1         1       1            1           <none>          87s


## too many pods

- if we check with `kubectl get pods` we see:
  - one pod for the deployment (named rng-xxxxxxxxxxxxxxxxxx-yyyyyy)
  - one pod per node for the daemon set named rng-zzzzzzz

NAME                             READY   STATUS    RESTARTS   AGE
pod/rng-7c7c6c8d74-m8hmq         1/1     Running   1          6h23m
pod/rng-h2cfb                    1/1     Running   0          87s

The daemon set created one pod per node
in a multi-node setup, masters usually have taints preventing pods from running there
(to schedule a pod on this node anyway, the pod will require appropriate tolerations)




## LINKS
https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/