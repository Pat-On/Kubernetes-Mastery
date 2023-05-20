# CNI Basics

## The container network interface (CNI)

- most kubernetes clusters use CNI plugins to implement networking
- when a pod is created, Kuibernetes delegates the network setup to these plugins
  - it can be a single plugin, or combination of plugins, each doing one task

- typically, CNI plugins will:
  - allocate an IP address (by calling an IPAM plugin)
  - add a network interface into the pod's network namespace
  - configure the interface as well as required routes etc.


## Multiple moving parts:

- the `pod-to-pod network` or `pod network`:
  - provides communication between pods and nodes
  - in generally implemented with CNI plugins

- the `pod-to-service network`: <--- previous exercise
  - provides internal communication and load balancing
  - is generally implemented with kube-proxy (or maybe kube-router)

- Network policies
  - provide firewalling and isolation
  - can be bundled with the `pod network` or provided by another component

## Even more moving parts
- inbpuind traffic can be handled by multiple components
  - something like kube-proxy or kube-router (for NodePort services)
  - load balancers (ideally, connected to the pod network)


- it is possible to use multiple pod networks in parallel
    (with meta-plugins like CNI-Genie or Multus)
- Some solutions can fill multiple roles
    (e.g. kube-router can be set up to provide the pod network and or network policies and or replace kube-proxy)

