# Creating a ConfigMap

## Exposing ConfigMaps to containers

- ConfigMaps can be exposed as plain files in the filesystem of a container
  - this is achieved by declaring a volume and mounting it in the container
  - this is particularly effective for ConfigMaps containing whole files
- ConfigMaps can be exposed as env variables in the container
  - this is achieved with Downward API
  - this is particularly effective for ConfigMaps containing individual parameters
- lets see how to do both

## Passing a configuration file with a ConfigMap
- we will start a load balancer powered by HAProxy
- we will use the official haproxy image
- it expects to find its configuration in `/usr/local/etc/haproxy/haproxy.cfg`
- we will provide a simple HAProxy configuration
- it listens on port 80, and load balances connections between IBM and Google


## Creating the ConfigMap

- Download our simple HAPProxy config:
  - `curl -O https:/k8smastery.com/haproxy.cfg`
- Create a ConfigMap named `haproxy` and holding the configuration file:
  - `kubectl create configmap haproxy --from-file=haproxy.cfg`
- check what out ConfigMap looks like:
  - `kubectl get configmap haproxy -o yaml`


## LINKS
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/
https://hub.docker.com/_/haproxy/