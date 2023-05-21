# Ingress Controller Port Config

## without `hostNetwork`
- normally each pod gets its own network namespace
  - sometimes called sandbox or network sandbox
- An IP address is assigned to the pod
- This IP address is routed/connected to the cluster network
- All containers of that pod are sharing that network namespace
  - and therefor using the same IP address

## with `hostNetwork: true`
- no network namespace gets created
- the pod is using the network namespace of the host 
- it `sees` and can use the interfaces and IP addresses of the host VM on macOS/win
- the pod can receive outside traffic directly, on any port
- Downside: with most network plugins, network policies would not work for that pod
    - most network policies work at the ip address level
    - filtering that pod = filtering traffic from the node


## What you will use now
- Docker Desktop
  - no build-in ingress installer, we will provide you yaml
  - ignores `hostNetwork` but service `type: LoadBalancer` works with `localhost`

- minikube
  - has a built-in NGINX installer `minikube addons enable ingress`
  - but lets use YAML we provided for learning purposes
  - `hostNetwork: true` enabled on pod works for minikube IP
- MicroK8s:
  - has a built-in NGINX installer `microk8s.enable ingress`
  - lets use YAML we provided anyway for learning purposes
  - `hostNetwork: true` enabled on pod works for Microk8s host ip