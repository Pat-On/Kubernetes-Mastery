# Editing Pod Labels


## Removing a pod from the load balancer

- Currently the `rng` service is defined by the `app=rng` selector
- the only way to remove a pod is to remove or change the `app` label
- .. but that will cause another pod to be created instead
- what is the solution?"

- We need to change the selector of `rng` service!
- lets add another label to that selector e.g. enables=yes


## complex Selector
- if a selector specifies multiple labels, they are understood as a logical AND
  - in other words the pods must match all the labels
- Kubernetes has support for advances, set-based selectors
  - but these cannot be used with services at least not yet



## The Plan
1. add the label `enabled=yes` to all our `rnd` pods
2. Update the selector for the `rng` service to also include enabled=yes
3. toggle traffic to a pod by manual adding/removing the `enabled` label
4. profit!

Note:
If we swap steps 1 and 2, it will cause a short service disruption, because there will be a period
of time during which the service selector would not match any pod.
during that time, requests to the service will time out. 
By doing things in the order above, we quarantee that there wont be any interruption


## Adding labels to pods

- we want to add the label `enabled=yes` to all pods that have `app=rng`
- we could edit each pod one by one with `kubectl edit ....`
- or we could use `kubectl label` to label them all
- `kubectl label` can use selectors itself

exercise:
- add `enabled=yes` to all pods that have `app=rng`:
  - `kubectl label pods -l app=rng enabled=yes`

```
pod/rng-7c7c6c8d74-m8hmq labeled
pod/rng-h2cfb labeled
```



## Updating the service selector
- we need to edit the service specification
- Reminder: in the service definition, we will see `app: rng` in two places
  - the label of the service itself (we do not need to touch that one)
  - the selector of the service (that is the one we want to change)

Exercise:
- update the service to add `enabled: yes` to its selector:
  - `kubectl edit service rng`


## when the YAML parser is being too smart
- YAML parsers try to help us:
  - xyz is the string "xyz"
  - 42 is the integer 42
  - yes is the boolean value true

- if we want the string "42" or the string "yes" we have to quote them
- so we have to use enabled: "yes"

For a good laugh if we had used 'ja' 'oui' 'si' as the value it would have work the same way ^^ 


## LINK: 
https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#kubectl-edit