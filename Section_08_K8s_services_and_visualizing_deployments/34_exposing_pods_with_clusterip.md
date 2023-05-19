# Exposing pods with clusterIP

## Running containers with open ports
- since `ping` does not have anything to connect to, we will have to run something else
- we could use the `nginx` official image but... we would not be able to tell the backends from each other
- we are going to use bretfisher/httpenv, a tiny HTTP server written in Go
- `bretfisher/httpenv` listens on port 8888
- it serves it environments variables in JSON format
- the nevironment variables will include `HOSTNAME` which will be the pod name
  (and therefor, will be different on each backend)


## Creating a deployment for out HTTP server

- in another window watch the pods to see when they are created
  - `kubectl get pods -w`

- Create a deployment for this very lightweight HTTP server:
  - `kubectl create deployment httpenv --image=bretfisher/httpenv`

- scale it to 10 replicas
  - `kubectl scale deployment httpenv --replicas=10`


`kubectl expose deployment httpenv --port 8888 `


```
\NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
httpenv      ClusterIP   10.96.226.195   <none>        8888/TCP   18s
kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP    25h
```

