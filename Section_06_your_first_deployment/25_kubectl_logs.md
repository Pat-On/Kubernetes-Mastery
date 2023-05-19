# kubectl logs

## viewing container output
- lets use the `kubectl logs` command
- we will pass either a pod name or a type/name
  (E./g if we specify a deployment or replica set, it will get the first pod in it)
- unless specified otherwise, it will only show logs of the first container in the pod (good thing there is only one in ours! )

Exercise:
- view the result of out `ping` command:
  - `kubectl logs deploy/pingpong`

in our case: `kubectl logs pod/pingpong`


## live tail

`kubectl logs --follow pod/pingpong`


Note:" what if we tried to scale `replicaset.apps/pingpong-XXXXXXXXXXX`?

We could! But the deployment would notice it right away, and scale back to the initial. 

Links:
https://kubernetes.io/docs/tasks/debug/
https://kubernetes.io/docs/concepts/cluster-administration/logging/



Important: you can't scale a pod. A pod doesn't have replicas. In this Lecture, you're scaling a deployment.


## streaming logs in real time
- just like `docker logs`, `kubectl logs` supports convenient options:
  - `f/--follow` to stream logs in real time (a la `tail -f`)
  - `--tail` to indicate how many lines you want to see (from the end)
  - `--since` to get logs only after a given timestamp

exercise:
- view the latest logs of our `ping` command:
  - `kubectl logs deploy/pingpong --tail 1 --follow`
- leave that command running, so that we can keep an eye on these logs


Links:
https://kubernetes.io/docs/concepts/cluster-administration/logging/
https://kubernetes.io/docs/tasks/debug/