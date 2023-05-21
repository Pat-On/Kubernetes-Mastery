# Deploying Traefik Ingress Controller

## Running Traefik on our cluster
- now lets deploy the Traefik Ingress Controller

- Apply the YAML
  - for docker desktop with Load Balancer
  - `kubectl apply -f https://k8smastery.com/ic-traefik-lb.yaml`

  - for minikube/MicroK8s with hostNetwork
  - `kubectl apply -f https://k8smastery.com/ic-traefik-hn.yaml`

- check the pod status
  - `kubectl describe -n kube-system ds/traefik-ingress-controller`


## it is working straight ahead because it using the same ingress resources that were used by nginx 
### NICE!!

## Links:
https://doc.traefik.io/traefik/providers/kubernetes-ingress/
https://slides.kubernetesmastery.com/#697