# Alternatives & Future of Ingress

## When not to use built-in Ingress resources

- you need features beyond ingress including:
  - tcp support, traffic splitting, mTLS, egress, service mesh
  - response transformation, routing to 2+ services


- You have external load balancers (like AWS ELBs) which route to NodePorts
- you do not need externally available HTTP services on the default ports


# Using CRD's  as alternative to Ingress resources

- due to the limits of the built-in ingress, many project are moving to CRD's
- for example, Traefik 2.x has a ingressRoute CRD option
- Ambassador a controller for Envoy proxy, uses a Mapping CRD
- These CRD proxy option do ingress plus more (sometimes called API Gateways)
  - TCP Support (anything beyond HTTP/HTTPS)
  - Traffic splitting, rate limiting, circuit breaking etc
  - Complex traffic routing, request and response transfomration
- Once we consider CRD's manyu more proxy option are available
  - envoy proxy based (gloo ambassador, contour)
  - other proxies (tyk, traefik, kong, krakenD)
- Eventually some more advanced features might be added to ingress resources
- we will cover more after we learn about CRD's and Operators
- 


## Links:
https://doc.traefik.io/traefik/providers/kubernetes-crd/