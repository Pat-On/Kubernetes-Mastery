# Replacing NGINX with Traefik

## Swapping NGINX for Traefik
- traefik is a proxy with built in kubernetes ingress support
- it has a web dashboard built-in lets encrypt full tcp support and more
- Most importantly: Traefik releases are named after cheeses

- We are going to use DaemonSet so that each node can accept connections
- We provided a YAML file which is essentially sum of:
  - Traefik's DaemonSet resource (patched with `hostNetwork` and tolerations)
  - Traefik's RBAC rules allowing it to watch necessary API object
- we will make a minor change to the YAML provided by Traefik to enable `hostNetworking` for MicroK8s and minikube
- for Docker Desktop we will add a `type: LoadBalancer` to the service


## Removing NGINX from our local cluster
- Before starting Traefik lets remove the nginx controller
- this won't remove Services or Ingress resources
- but it will make them unavailable from outside the cluster


- Delete our NGINX controller and related resources:
    - for docker dektop with LoadBalancer
    - `kubectl delete -f https://k8smastery.com/ic-nginx-lb.yaml`

    - for minikube/MicroK8s with hostNetork
    - `kubectl delete -f https://k8smastery.com/ic-nginx-hn.yaml`

- also remove the redirect ingress resource. it only worked in nginx
  - `kubectl delete -f https://k8smastery.com/redirect.yaml`


## Links
https://traefik.io/traefik/