# Rollout History

## in this specific scenario
- our version numb are easy to quess
- what if we had used git hashes
- what if we had changed other parameters in the Pod spec?

## Listing versions
- we can list successive versions of a Deployument with `kubectl rollout history`

exercise:
check it out! 
`kubectl rollout history deployment worker`

we do not see all revisions.
we might see something like 1, 4, 5
(Depending on how many undos we did before )

replica-set and deployment are different resources and have separated history

## Explaining deployment revisions
- these revisions correspond to our ReplicaSets
- this information is stored in the replicaSet annotations

check:
kubectl describe replicasets -l app=worker | grep -A3 Annotations

```
Annotations:    deployment.kubernetes.io/desired-replicas: 10
                deployment.kubernetes.io/max-replicas: 13
                deployment.kubernetes.io/revision: 4
                deployment.kubernetes.io/revision-history: 2
--
Annotations:    deployment.kubernetes.io/desired-replicas: 10
                deployment.kubernetes.io/max-replicas: 13
                deployment.kubernetes.io/revision: 1
Controlled By:  Deployment/worker
--
Annotations:    deployment.kubernetes.io/desired-replicas: 10
                deployment.kubernetes.io/max-replicas: 13
                deployment.kubernetes.io/revision: 3
Controlled By:  Deployment/worker
```

## What about the missing revisions?
- the missing revisions are stored in another annotation:
  - `deployment.kubernetes.io/revision-history`
- these are not shown in `kubectl rollout history`
- we could easily reconstruict the full list with a script (if we wanted to!)

## Rolling back to an older version

- `kubectl rollout undo` can work with a revision number

rollback to the known good deployment versions:
    `kubectl rollout undo deployment worker --to-revision=1`

- check the web UI or the list of pods

## LINKS:
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#revision-history-limit
https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
https://www.weave.works/blog/how-many-kubernetes-replicasets-are-in-your-cluster-