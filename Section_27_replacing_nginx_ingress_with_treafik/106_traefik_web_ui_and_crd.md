# Traefik Web UI and CRD

## Traefik web UI

- Traefik provides a web dashboard on container port 8080
- for those using the 'loadBalancer` method (Docker Desktop) it is enabled

- for those using `hostNetwork` this could be a problem
- the container won't start if anything is listening on `< host IP >: 8080`
- on MicroK8s, Kubernetes API runs on 8080
- for those using minikube you can un-comment the yaml and re-apply 
- you could also edit the resource(s) and manually add the details e.g
  - `kubectl edit -n kube-system ds/traefik-ingress-controller`


## What about Traefik 2.x IngressRoute resources?
- we have been using Traefik 2.X as the ingress controller
- Traefik released 2.0 in late 2019
- their documentation talks about IngressRoute resource 
- but IngressRoute is not a built-in resource of Kubernetes
- Traefik 2.x now support a custom CRD (Custom Resource Definition)
- we will explore why in a bit




## Links
https://doc.traefik.io/traefik/operations/dashboard/