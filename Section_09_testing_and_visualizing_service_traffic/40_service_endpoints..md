# Service Endpoints


## Services and endpoints
- a service has a number of endpoints
- each endpoints is a host + port where the service is available
- the endpoints are maintained and updated automatically by Kubernetes

exercise:
check the endpoints that kubernetes has associated with out httpenv service:
`kubectl describe service httpenv`

in the output, there will be a line starting with `endpoints`
that line will list a bunch of addresses in `host:port` format

## viewing endpoints details

- when  we have many endpoints, our display commands truncate the list
  - `kubectl get endpoints`
- if we want to see the full list, we can use a different output:
  - `kubectl get endpoints httpenv -o yaml`

- there IP addresses should match the addresses of the coresponging pods:
  - `kubectl get pods -l app=httpenv -o wide`


## endpoints not endpoint

- endpoint is the only resource that cannot be singular
-  there is because the type itself is plural (unlike every other resource)
-  there is no endpoint object type Endpoints struct
-  the type does not represent a single endpoint but a list of endpoints

(We will see NodePorts and Ingresses more in detail later)

Links:
https://kubernetes.io/docs/tutorials/services/connect-applications-service/#creating-a-service