# What makes up Ingress?

## Ingress resources
- Kubernetes API resource `kubectl get ingress/ingresses/ing`
- designed to expose HTTP services
- basic features
  - load balancing
  - SSL termination
  - name-based virtual hosting

- Can also route to different services depending on:
  - URI path `/api` -> `api-service`, `/static` -> `assets-service`
  - client headers including cookies (forA/B testing, canary deployment...)
  - and more! 


# Principle of operation

- Step 1: deploy an ingress controller
  - ingress controller = load balancing proxy + control loop
  - the control loop watches over ingress resources and configures the LB accordingly
  - these might be two separate processes (NGINX server + NGINX Ingress controller)
  - or a single app that knows how to speak to Kubernetes API (Traefik)


- Step 2: set up DNS (usually)
  - associate external DNS entries with the load balancer or host address

- Step 3: create ingress resources for our Service resources
  - these reources contain rules for handling HTTP/S connections
  - the ingress  controller picks up these resources and cofigure the LB
  - connections to the ingress LB will be processed by the rules 

```

    API         CONTROLLER MANAGER
    |                       |-> Deployment Controller 
    |                                   |
    Deployment <------------------------
    |
    |
    Ingress Resource                NGINX Ingress
        ^                               Controller
        |----------------------------------|


```



## Links:
https://kubernetes.io/docs/concepts/services-networking/ingress/
https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/
https://kubernetes.io/docs/concepts/overview/components/#control-plane-components