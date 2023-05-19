# K8s newer namespaces

## what about `kube-public`

- list the pods in the `kube-public` namespace:
  - `kubectl -n kube-public get pods`

nothing

- `kube-public` is created by out installer and used for security bootstrapping


## Exploring `kube-public`
- the only interesing object in kube-public is a ConfigMap names `cluster-info`


exercise:
- list ConfigMap objects:
  - `kubectl -n kube-public get configmaps`
- inspect cluster-info
  - `kubectl -n kube-public get configmap cluster-info -o yamls`

note:
the `selfLink` URI: `/api/v1/namespaces/kube-public/configmaps/cluster-info`
we can use that (later in `kubectl context` lectures)


# what about `kube-node-lease`?
- starting with kubernetes 1.14 there is a kube-node-lease namespace
  (or in kuberentes 1.13 if the NodeLease feature gate is enabled)
- that namespace contains one Lease object per node
- node leases are a new way to implement node heartbeats
   (i.e. node regularly pinging the control plane to say 'I am alive!')
- for more details see KEP-009 or the node controller documentation
