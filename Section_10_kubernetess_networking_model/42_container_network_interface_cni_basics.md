# Kubernetes Network Model

- TL, DR
  - Our cluser (nodes and pods) is one big  flat IP network

- in detail:
  - all nodes must be able to each each other, without NAT
  - all pods must be able to each each other, without NAT
  - pods and nodes must be able to reach each other, without NAT
  - each pod is aware of its IP address (no NAT)
  - pod IP addresses are assigned by the network implementation
- kubernetes does not mandate any particular implementation

## Kubernetes network model: the good
- everything can rach everything
- no address translation
- no port translation
- no new protocol
- the network implementation can decide how to allocate addresses
- ip addresses do not have to be portable from a node to another
  - for example we can use a subnet per node an use a simple routed topology
- the specification is simple enough to allow many various implementations


## Kubernetes network modes: the less good
- Everything can reach everythinbg
  - if you want security you need to add network policies
  - the network implementation you use need to support them

- there are literally dozens of implementations out there
  - 15 are listed in the kubernetes documenation
- pods have level 3 (IP) connectivity, but services are level 4 (TCP or UDP)
    (services map to a single UDP or TCP port, no port ranges or arbitrary IP packets)
- `kube-proxy` is on the data path when connecting to a pod or container, 
  - and it is not particulary fast (relies on userland proxying or iptables)

## Kubernetes network model: in practice
- the nodes we are using have been set up to use kubenet, calico or something else
- do not worry about the warning about `kube-proxy` performance
- unless you
  - routinely saturate 10G network interfaces
  - count packet rates in millions per seconds
  - run high-traffic VOIP or gaming platforms
  - do weird things that involve millions of simultaneous connections
    - (in which case you are already familiar with kernel tuning)
- if necessary, there are alternative to `kube-proxy` eg: `kube-router`


Links:
https://kubernetes.io/docs/concepts/cluster-administration/networking/
https://www.kube-router.io/
https://en.wikipedia.org/wiki/OSI_model