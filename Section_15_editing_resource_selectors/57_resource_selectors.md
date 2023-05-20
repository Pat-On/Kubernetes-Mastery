# Resource Selector

## Updating load balancer configuration

- we would like to remove a pod from the load balancer
- what would happen if we removed that pod with `kubectl delete pod...`?
  - It would be re-created immediately (by the replica set or the daemon set)
- what would happen if we removed the `app=rng` label from that pod
  - it would also be re-created immediately WOW!
  - 


WHY?

## Selectors for replica sets and daemon sets

- the mission of replica set is: 
  - Make sure that there is the right number of pods matching this spec

- the mission of a daemon set is:
  - make sure that there is a pod matching this spec on each node!

- in fact replica sets and daemon sets do not check pod specifications
- they merely have a selector, and they look for pods matching that selector
- yes we can fool them by manually creating pods with the right labels
- bottom line if we remove our `app=rng` label....
  - the pod disappears for its parent which re-creates another pod to replace it

## isolation of replica sets and daemon sets

- since both the `rng` daemon set and the `rng` replica set use `app=rng` ...
  - why do not they find each other's pods?

- Replica sets have a more specific selector, visible with `kubectl describe`
  - it looks like `app=rng, pod-template-hash=abcd1234`
- Daemon sets also have a more specific selector, but it is invisible
  - it looks like `app=rng, controller-revision-hash=abcd1234
- as a result each controller only sees the pods it manages

## Links:
https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/
https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/