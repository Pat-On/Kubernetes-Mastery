# First contact with Kubectl


- kubectl is (almost) the only tool we will need to talk to kubernetes
- it is a rich CLI tool around the Kubernetes API
  (everything you can do with kubectl, you can do directly with the api)
- on our machines there is a ~/.kube/config file with
  - the kubernetes API address
  - the path to out TLS certificates used to authenticate
- you can also use the --kubeconfig flag to pass a config file
- or directly --server, --user etc


# kubectl get

- lets look at our Node resources with kubectl get

- look at the composition of our cluser:
  - kubectl get node

- these commands are equivalent:
  - kubectl get no
  - kubectl get node
  - kubectl get nodes


- kubectl get can output JSON yaml or be directly formatted

- give us more info about the nodes:
  - kubectl get nodes -o wide

- lets have some yaml
  - kubectl get no -o yaml
  - see that kind: list at the end? it is the type of our result


(AB) using kubectl and jq

- it is super easy to build custom reports
- show the capacity of all our nodes as a stream of JSON objects
- kubectl get nodes -o json |
            jq ".items[] | {name:.metadata.name} + .status.capacity"







# Links:
https://kubernetes.io/docs/reference/kubectl/