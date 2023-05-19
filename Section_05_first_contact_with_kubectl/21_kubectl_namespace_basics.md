# Namespaces

- namespaces allow us to segregate resources

- list the namespaces on our cluster with one of these commands:
  - `kubectl get namespaces`
  - `kubectl get namespace`
  - `kubectl get ns`

```
pat@pat-GE62-2QF:~/Projects/kubernetes-mastery$ kubectl get ns
NAME              STATUS   AGE
default           Active   18h
kube-node-lease   Active   18h
kube-public       Active   18h
kube-system       Active   18h
```

- by default, `kubectl` uses the `default` namespace
- we can see resources in all namespaces with `--all-namespaces`

exercise:
- list the pods in all namespaces:
  - `kubectl get pods --all-namespaces`
- since kubernetes 1.14, we can also use -A as a shorter version
  - `kubectl get pods -A`

```
kube-system   coredns-565d847f94-8l5xj                 1/1     Running   1 (75m ago)    18h
kube-system   coredns-565d847f94-x8skd                 1/1     Running   1 (75m ago)    18h
kube-system   etcd-docker-desktop                      1/1     Running   1 (75m ago)    18h
kube-system   kube-apiserver-docker-desktop            1/1     Running   1 (75m ago)    18h
kube-system   kube-controller-manager-docker-desktop   1/1     Running   1 (75m ago)    18h
kube-system   kube-proxy-n7ddz                         1/1     Running   1 (75m ago)    18h
kube-system   kube-scheduler-docker-desktop            1/1     Running   1 (75m ago)    18h
kube-system   storage-provisioner                      1/1     Running   2 (74m ago)    18h
kube-system   vpnkit-controller                        1/1     Running   11 (14m ago)   18h
```


# what are all these control plane pods?
- `etcd` is our etcd server
- `kube-apiserver` is the api server
- `kube-controller-manager` and `kube-scheduler` are other control plane components
- `coredns` provides DNS-based service discovery (replacing kube-dns as of 1.11)
- `kube-proxy` is the (per-node) component managing the network overlay
- the ready column indicated the number  of containers in each pod
- note: this only shows containers, you wont see host svcs (eg . microk8s)
- also note you may see different namespaces depending on setup


# Scoping another namespace (for now think about it as a 'filter' )
- we can also look at a different namespace (other than default)

- list only the pods in the `kube-system` namespace
  - `kubectl get pods --namespace=kube-system`
  - `kubectl get pods -n kube-system`


# namespace and other kubectl commands
- we can use -n/--namespace with almost every kubectl command
- example
  - `kubectl create --namespace=x` to create something in namespace X
- we can use -A/--al-namespaces with most commands that manipulate multiple object
- Example:
  - `kubectl delete` can delete resources across multiple namespaces
  - `kubectl label` can add/remove/update labels across multiple namespaces

