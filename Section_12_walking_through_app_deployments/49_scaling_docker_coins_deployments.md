# Scaling DockerCoins Deployments


## Scaling our demo app
- our ultimate goal is to get more DockerCoins
- ie increase the number of loop per second shown on the web uo
- lets look at the architecture again:

- summary: worker is doing the most of the job

- we are at 4 hashes a second. lets ramp this up
- the loop is done in the worker, perhaps we could try adding more workers?


## Adding another worker
- all we have to do is sacale the worker deployment
- Exercise:
  - open two new terminal to check what is going on with pods and deployments:
    - `kubectl get pods -w`
    - `kubectl get deployments -w`

  - now create more `worker` replicas:
    - `kubectl scale deployments worker --replicas=2`

- The graph will peak at 10 hashes/second
- we can add as many workers at we want: we will never go past 10 hashes/seconds

## Links:
https://kubernetes.io/docs/tasks/manage-kubernetes-objects/update-api-object-kubectl-patch/