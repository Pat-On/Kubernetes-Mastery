# YAML From Scratch

## Writing YAML from scratch, "YAML THE HARD WAY"

- A reminder about manifests
  - each file contains one or more manifests
  - each manifest describes an api objects (deployment, service etc)
  - each manifest needs four parts (root key: values in the file)

apiVersion      find with` kubectl api-versions`
kind            find with `kubectl api-resources`
metadata
spec            find with` kubectl describe pod`


## General workflow of YAML from scratch

- find the resource `kind` you want to create (`api-resources`)

```
daemonsets                        ds           apps/v1   
pods                              po           v1           
```

- find the latest `apiVersion` your cluster support for `kind` (`api-versions`)
- `kubectl api-versions`
- give it a `name` in metadata (minimum)
- Dive into the `spec` of that `kind`
  - `kubectl explain <kind>.spec`
  - `kubectl explain <kind> --recursive`
- browse the docs API Reference for your cluster version to supplement
- `kubectl explain pod`
- `kubectl explain pod.spec`
- `kubectl explain pod.spec.volumes`
- use `--dry-run` and `--server-dry-run` for testing
- `kubectl create` and  `delete` until you get it right

 
```
admissionregistration.k8s.io/v1
apiextensions.k8s.io/v1
apiregistration.k8s.io/v1
apps/v1
authentication.k8s.io/v1
authorization.k8s.io/v1
autoscaling/v1
autoscaling/v2
autoscaling/v2beta2
batch/v1
certificates.k8s.io/v1
coordination.k8s.io/v1
discovery.k8s.io/v1
events.k8s.io/v1
flowcontrol.apiserver.k8s.io/v1beta1
flowcontrol.apiserver.k8s.io/v1beta2
networking.k8s.io/v1
node.k8s.io/v1
policy/v1
rbac.authorization.k8s.io/v1
scheduling.k8s.io/v1
storage.k8s.io/v1
storage.k8s.io/v1beta1
v1
```







## LINKS

https://kubernetes.io/docs/reference/
https://github.com/kelseyhightower/kubernetes-the-hard-way