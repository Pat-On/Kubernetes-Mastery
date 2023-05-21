# Why do we need ingress?

## Exposing HTTP services with ingress resources
- services give us a way to access a pod or a set of pods
- services can be exposed to the outside world
  - with type `NodePort` on a port > 30 000
  - with type `LoadBalancer` allocating an external load balancer
- what about http services
  - how can we expose `webui` `rng` `hasher`
  - the kubernetes dashboard?
  - all on the same IP and port"?

## Exposing HTTP services
- if we use `NodePort` services clients have to specify port numbers
  - ie. http://xxxxx:31444

- `LoadBalancer` services are nice, but:
  - they are not available in all env
  - they often carry an additional cost (e.g. they provision an ELB)
  - they often work at OSI Layer 4 (IP+Port) and not Layer 7 (HTTP/S)
  - they require one extra step for DNS integration
    - waiting for the `LoadBalancer` to be provisioned; then adding it to DNS
  

  - We could build our own reverse proxy


## Building a custom reverse proxy
- there are many options available":
  - Apache
  - HAProxy
  - Envoy Proxy
  - Gloo
  - Nginx
  - Traefik
- Most of these options require us to update/edit configuration files after each change
- some of them can pick up virtual hosts and backends from a configuration store
- would not it be nice if this configuration could be managed with the Kubernetes API
- Ingress Resources - Answer 

## ingress vs Ingress

ingress
- ingress definition: going in entering, the opposite of egress leaving
- in networking terms, ingress refers to handling incoming connections
- could imply incoming to firewall, network or in this case, a server cluster

Ingress
- Ingress (capital I) in these slides means the kubernetes ingress resource
- specific to HTTP/S


