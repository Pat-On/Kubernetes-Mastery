# Using a Config Map

- We are going to use the following pod definition

```
apiVersion: v1
kind: Pod
metadata:
    name: haproxy
spec:
    volumes:
    - name: config
    configMap:
        name: haproxy
    containers:
    - name: haproxy
      image: haproxy
      volumeMounts:
      - name: config
        mountPath: /usr/local/etc/haproxy/
```

## Using the Config Map
- apply the resource definition from the previous slide

Exercise:
- create the HAProxy pod:

`kubectl apply -f https://k8smastery.com/haproxy.yaml`

- check the ip address allocated to the pod, inside `shpod`:

`kubectl attach --namespace=shpod -ti shpod`
`kubectl get pod haproxy -o wide`
`IP=$(kubectl get pod haproxy -o json | jq -r .status.podIP)`


## Testing our load balancer

- the load balancer will send
  - halfd of the connections to google 
  - other half to ibm

access the load balancer of a few times
curl $IP

- we should see connections server by Google and others served by IBM.
- each server sends us a redirect page. Look at the URL that they send us to! 