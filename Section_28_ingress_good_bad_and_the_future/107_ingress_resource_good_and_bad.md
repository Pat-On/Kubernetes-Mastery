## Using multiple ingress controller
- you can have multiple ingress controller active simultaneously
  - Traefik, Gloo and Nginx
- You can even have multiple instances of the same controller
  - one for internal another for external traffic
- The `kubernetes.io/ingress.class` annotation can be used to tell which one to use 
- It is ok if multiple ingress controllers configure the same resource
  -  it just means that the service will be accessible through multiple paths

## ingress resources the good
- the traffic flows directly from the ingress load balancer to the backend
  - it does not need to go through the `clusterIP`
  - in fact we do not even need a clusterIP we can use a headles service

- The load balancer can be outside of Kubernetes
  - as long as it has access to the cluster subnet
- this allows the use of external (hardware, physical machines...) load balancers
- annotations can encode special features
  - rate-limiting, A/B testing, sessions stickiness 

## Ingress resources: the bad (cough annotations cough)
- Aforementioned 'special features' are not standardized yet
- some controllers will support them; some would not
- even relatively common features (stripping a path prefix)_ can differ:
  - traefik.ingres.kubernetes.io/rule-type:PathPrefixStrip
  - ingress.kubernetes.io/rewrite-target: /
- this should eventually stabilize
- annotation are not validated in CLI - they are consider as a metadata
- some proxies provide a CRD (custom resource definition) option
- 