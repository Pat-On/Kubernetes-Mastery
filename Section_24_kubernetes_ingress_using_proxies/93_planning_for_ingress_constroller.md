# Planning for NGINX Ingress Controller

## Ingress in action: NGINX
- we will deploy the NGINX Ingress Controller first
  - this is a popular, yet arbitrary choice, the docs list over a dozen options

- For DNS we will use nip.io
  - *.127.0.0.1.nip.io resolves to 127.0.0.1
  - we do this so we can use various FQDN's without editing our `hosts` file
  - we will create ingress resources for various HTTP-based Services


## Deploying pods listening on port 80
- we want our Ingress load balancer to be available on port 80
- we could do that with a `LoadBalancer` service
  - .. but it requires support from the underlying infrastructure
  - minikube and MicroK8s do not work with it
  - .. but Docker Desktop supports it for localhost
- We could use pods specifying `hostPort: 80`
  - but with most CNI plugins this does not work or requires additional setup
- We could use a `NodePort` service
  - but that requires changing the `--service-node-port-range` flag in the api server
- Last resort: the `hostNetwork` mode

## Links: 
https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/#additional-controllers
https://docs.google.com/spreadsheets/d/1DnsHtdHbxjvHmxvlu7VhzWcWgLAn_Mc5L1WlhLDA__k/edit#gid=0