# Recovering Failed Updates

## checking the dashboard during the bad rollout

`kubectl describe deploy worker > deployment.txt`


## Recovering from a bad rollout
- we could push some v0.3 image
  - the pod retry logic will eventually catch it and the rollout will proceed
- or we could invoke a manual rollback


exercise:
kubectl rollout undo deploy worker
kubectl rollout status deploy worker

output: deployment "worker" successfully rolled out

## rolling back to an older version
- we reverted to v0.2
- but this version still has a performance problem
- how can we get back to previous version?

# multiple undos do not work
- if we see successive versions as a stack:
  - kubectl rollout undo does not pop the last element from the stack
  - it copies th N-1th element to the top
- multiple undos just swap back and forth between the last two version 


`kubectl rollout undo deployment worker`




## Links
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment