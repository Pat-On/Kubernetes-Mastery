# Labels and Selectors

- the `rng` service is load balancing requests to a set of pods
- that set of pods is defined by the selector of the `rng` service

exercise 
check the selector in the `rng` service def9inition
`kubectl describe service rng`


- the selector is `app=rng`
- it means all the pods having the label `app=rng`
- they can have additional labels as well, that is ok!
- two different resources but the same service!

```
Name:              rng
Namespace:         default
Labels:            app=rng
Annotations:       <none>
Selector:          app=rng    <--- it is like glue that is sticking services together (selector)
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.100.114.206
IPs:               10.100.114.206
Port:              <unset>  80/TCP
TargetPort:        80/TCP
Endpoints:         10.1.0.175:80,10.1.0.193:80
Session Affinity:  None
Events:            <none>
```

But.. why do these pods (in particular, the new ones) have this `app=rng` label?

## Selector Evaluation
- we can use selectors with many `kubectl` commands
- for instance with `kube3ctl get` `kubectl logs` `kubectl delete` and more

exercise:
get the list of pods matching selector `app=rng`

`kubectl get pods -l app=rng`
`kubectl get pods --selector app=rng`

But.. why do these pods (in particular, the new ones) have this `app=rng` label?


## Where do labels come from?
- when we create a deployment with `kubectl create deployment rng` this deployment gets the label `app=rng`
- the replica sets created by this deployment also get the label `app=rng`
- the pods created by these replica sets also get the label `app=rng`
- when we created the daemon set from the deployment, we re-used the same spec <--- reason
-  therefor, the pods created by the daemon set get the same label
- when we use `kubectl run stuff` the label is `run=stuff` instead




## LINKS
https://kubernetes.io/docs/reference/labels-annotations-taints/
https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/