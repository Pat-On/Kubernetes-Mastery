# DaemonSets

- We want to scale `rng` in a way that is different from how we scaled `worker`
- we want one (and exactly one) instance of `rng` per node
- we do not want two instances of `rng` on the same node
- we will do that with daemon set

## why not a deployment?

- can not we just do `kubectl scale deployment rng --replicas=...`?
- nothing quarantees that the `rng` containers will be distributed evenly
- if we add nodes later, they will not automatically run a copy of `rng`
- if we remove (or reboot) a node, one `rng` container will restart elsewhere
    and we will end up with two instances `rng` on the same node



## deamon sets in practice

- daemon sets are great for cluster-wide, per node processes
  - `kube-proxy`
  - CNI network plugins
  - monitoring agents
  - hardware management tools (eg SCSI/FC HBA agents)
  - etc
- They can also be restricted to run only on some nodes


## creating a daemon set

- unfortunately as of kubernetes 1.15 the CLI cannot create daemon sets
- more precisely: it does not have a subcommand to create a daemon set
- but any kind of resource can always be created by providing a YAML description
- `kubectl apply -f foo.yaml`

- HYow do we create the YAML file for our daemon set?
  - option 1: read the docs
  - option 2: vi our way out of it


## Links
https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/#create-a-daemonset
https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/#running-pods-on-only-some-nodes
https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/
