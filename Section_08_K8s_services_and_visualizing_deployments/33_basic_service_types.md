# Basic Server Types

## Exposing containers

- `kubectl expose` creates a service for existing pods
- a service is a stable address for a pod (or a bunch of pods)
- if we want to connect to our pod(s) we need to create a service
- one a service is created, CoreDNS will allow us to resolve it by name
  (ie after creating service `hello`, the name `hello` will resolve to something)
- there are different types of services, detailed on the following slides:
  - `clusterIP`
  - `NodePort`
  - `LoadBalancer`
  - `ExternalName`

## Basic Services Types

- ClusterIP (default type)
  - a virtual IP address is allocated for the service (in an internal, private range)
  - this IP address is reachable only from within the cluster (nodes and pods)
  - our code can connect to the service using the original port number

- NodePort (accessible outside of the cluster - very good for backed services)
  - a port is allocated for the service (by default in the 30.000 - 32.768 range)
  - that port is made available on all our nodes and anybody can connect to it
  - our code must be changed to connect to that new port number

these service types are always available

under the hood: `kube-proxy` is using a userland proxy and bunch of `iptables` rules

- LoadBalancer
  - an external load balancer is allovated for the service
  - the load balancer is configured accordingly
    (eg a `NodePort` service is created, and the load balancer send traffic to that port)
  - available only when the underlying infrastructure provides some "load balancer as a service
    - eg: aws, azure, gce, openstack

- ExternalName
  - the DNS entry managed by CoreDNS will just be a `cname`  to a provided record
  - no port no ip address, no nothing else is allocated
