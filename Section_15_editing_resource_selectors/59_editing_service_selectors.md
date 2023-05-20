# Editing Service Selectors


## updating the service selector, take 2

exercise 
update the service to add `enabled: "yes"` to its selector:
`kubectl edit service rng`


this time it should work! 
if we did everything correctly the web UI should not show any change

## Updating labels
- we want to disable the pod that was created by the deployment
- all we have to do is remove the enabled label from that pod
- to identify that pod we can use its name
- or rely on the fact that it is the only one with a `pod-template-hash` label
- good to know
  - `kubectl label ... foo=` does not remove a label it sets it to an empty string
  - to remove label foo use `kubectl label ... foo-`
  - to change an existing label we would need to add `--overwrite`


## Removing a pod from the load balancer

exercise:
- in one windows, check the logs of that pod:
  
  POD=$(kubectl get pod -l app=rng,rng-7c7c6c8d74-m8hmq -o name)
  POD=$(kubectl get pod -l app=rng,pod-template-hash -o name)

  
  kubectl logs --tail 1 --follow $POD

  We should see a steady stream of HTTP logs

- in another window remove the label from the pod:
  kubectl label pod -l app=rng,pod-template-hash enabled-

  the stream of HTTP logs should stop immediately


  there might be a slight change in the web ui (since wer removed a bit of capacity from `rng` service
  ) if we remove more pods the effect should be more visible


  side note:
  `kubectl label pod -l app=rng,pod-template-hash enabled="yes"`

  this is going to add the value again and start logs/traffic again


  ## Updating the daemon set

  - if we scale up our cluster by adding new nodes, the daemon set will ceate more pods
  - these pods won't have enabled=yes label
  - if we wanmt these pods to have that label we need to edit the daemon set spec
  - we can do that with e.g. `kubectl edit daemonset rng`


