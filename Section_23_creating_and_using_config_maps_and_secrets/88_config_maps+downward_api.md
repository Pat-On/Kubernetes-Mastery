# ConfigMaps & Downward API

## Exposing ConfigMaps with the Downward API
- we are going to run a Docker registry a custom port
- by default the registry listens on port 5000
- this can be changed by setting env var `REGISTRY_HTTP_ADDR`
- we are going to store the port number in a ConfigMap
- Then we will expose that ConfigMap as a container env var

##  Creating the configMap

- our ConfigMap will have a single key: `http.addr`:
  - `kubectl create configmap registry --from-literal=http.addr=0.0.0.0:80`
- check our ConfigMap:
  - `kubectl get configmap registry -o yaml`

## Using the ConfigMapo

We are going to use the following pod definition:

```
apiVersion: v1
kind: Pod
metadata:
  name: registry
spec:
  containers:
  - name: registry
    image: registry
    env:
    - name: REGISTRY_HTTP_ADDR
      valueFrom:
        configMapKeyRef:
          name: registry
          key: http.addr

```


## 

`kubectl apply -f https://k8smastery.com/registry.yaml`

- check the ip address allocated to the pod, inside `shpod`:

`kubectl attach --namespace=shpod -ti shpod`
`kubectl get pod registry -o wide`
`IP=$(kubectl get pod registry -o json | jq -r .status.podIP)`

- Confirm that the rteistry is available on port 80
- `curl $IP/v2/_catalog`