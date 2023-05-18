https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/
https://etcd.io/

## Kubernetes architecture: the nodes
- the nodes executing our containers run a collection of services:
  - a container engine typically docker
  - kubelet the node agent
  - kub-proxy a necessary but not sufficient network component

- nodes were formerly called minions
  - You might see that word in older articles or documentation


- the kubernetes logic (its brains) is a collection of services:
  - the api server (our point of entry to everything!)
  - core services like the scheduler and controller manager
  - etcd ( a highly available key/value store; the 'database' of kubernetes)

- together these services form the control plane of our cluster
- the control plane is also called the master

## Running the control plane on special nodes
- it is common to reserve a dedicated node for the control plane
- (except for single-node development clusters like when using minikube)
- this node is then called a master (yes this is ambiguous is the master a node or the whole control plane?)
- normal applications are restricted from running on this node (by using a mechanism called taints)
- when high availability is required, each service of the control plane must be resilient
- the control plane is then replicated on multiple nodes (this is sometimes called a multi-master setup)

## Running the control plane outside containers
- the services of the control plane can run in or out of containers
- for instance: since etcd is a critical service, some people deploy it directly on a dedicated cluster (without containers) (This is illustrated on the first super complicated schema)
- in some hosted kubernetes offerings eg AKS, GKE  EKS the control plane is invisible ( we only 'see' a kubernetes API endpoint)
- in that case there is no master node

for this reason it is more accurate to say 'control plan' rather than 'master'

