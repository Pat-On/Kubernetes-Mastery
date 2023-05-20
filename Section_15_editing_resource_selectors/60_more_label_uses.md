# More Label Uses

## We have put resources in your resources

- reminder: a daemon set is a resource that creates more resources!
- there is a difference between:
  - the label(s) of a resource in the `metadata` block in the beginning
  - the selector of a resource in the `spec` block
  - the labels of the resources created by the first resource in the `template ` block

- we would need to update the selector and the template
  - metadata labels are not mandatory

- the template must match the selector
  - ie the resource will  refuse to create resource that it will not select 


## Labels and Debugging
- when a pod is misbehaving, we can delete it: another one will be recreated
- but we can also change its labels
- it will be removed from the load balancer (it wont receive traffic anymore)
- another pod will be recreated immediately
- but the problematic pod is still here and we can inspect and debug it
- we can even re-add it to the rotation if necessary
  - very useful to troubleshoot intermittent and elusive bugs


## Labels and advances rollout control
- conversely we can add pods matching a service's selector
- these pods wil then receive requests and serve traffic
- examples:
  - one-shot pod with all debug flags enabled to collect logs
  - pods created automatically but added to rotation in a second step by setting their label accordingly
- this gives us building blocks for canary and blue/green deployments <- INTERESTING!


## Cleanup 

kubectl delete -f https://k8smastery.com/dockercoins.yaml &&
kubectl delete daemonset/rng