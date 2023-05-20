# Creating DockerCoins

## running DockerCoins on kubernetes
- we can now deploy pir code (as well as a redis instance)

exercise:
- Deploy `redis`
  - `kubectl create deployment redis --image=redis`

- Deploy everything else:
  - `kubectl create deployment hasher --image=dockercoins/hasher:v0.1`
  - `kubectl create deployment rng --image=dockercoins/rng:v0.1`
  - `kubectl create deployment webui --image=dockercoins/webui:v0.1`
  - `kubectl create deployment worker --image=dockercoins/worker:v0.1`


## is this working?
- after waiting for the deploym,,ent to complete lets look at the logs
  - `kubectl get deploy -w ` to watch deployments events

look at some logs
`kubectl logs deploy/rng`
`kubectl logs deploy/worker`


## we need to expose the servers - dns

## Connecting containers together

- Three deployments need to be reachable by others `hasher` `redis` `rng`
- `worker` does not need to be exposed
- `webui` will be dealt with later

Exercise:
Expose each deployment, specifying the right port

`kubectl expose deployment redis --port 6379`
`kubectl expose deployment rng --port 80`
`kubectl expose deployment hasher --port 80`