# Healthcheck Basics

 - healthchecks are key to providing built-in lifecycle automation
 - healthchecks are probes that apply to containers (not to pods)
 - kubernetes will take action on container that fail healthchecks
   - liveness - is the container dead or alive? (most important probe)
   - readiness - is this container ready to serve traffic (only needed if a service)
   - startup - is this container still starting up

- different probe handlers are available (http, tcp, program execution)
- everything is handled by kubelet node that exists on each node
- they do not replace a full monitoring solution
- lets see the different and how to use them!


## liveness probe

- indicates if the container is dead or alive
- a dead container cannot come back to life
- if the liveness probe fail, the container is killed
- to make really sure that it is really dead; no zombies or undeads!
- what happens next depends on the pod's `restartPolicy`
  - `never` the container is not restarted
  - `OnFailure` or `Always`: the container is restarted


## When to use a liveness probe
- to indicate failures that can not be recovered
  - deadlocks (causing all requests to time out)
  - internal corruption (causing all requests to error)
- anything where our incident response would bne `just restart/ reboot it`
- do not use liveness probes for problem that can not be fixed by a restate
- otherwise we just restart our pods for no reason, creating useless load


## readiness probe
- indicates if the container is ready to serve traffic
- if a container becomes 'unready' it might bew ready again soon
- if the readiness probe fails:
  - the container is not killed
  - if the pod is a member of a service it is temporary removed
  - it is re-added as soon as the readiness probe passes again 

## when to use a readiness probe
- to indicate failure due to an external cause
  - database is down or unreachable
  - mandatory auth or other backend service unavailable
- to indicate temporary failure or unavailability
  - application can only service N parallel connections
  - runtime is busy doing garbage collection or initial data load

## startup probe 
- kubernetes 1.16 introduces a third type of probe: `startupProbe`
  - it is in alpha in kubernetes 1.16
- it can be used to indicate `container not ready yet`
  - process is still starting
  - loading external data, priming caches
- before k8s 1.16 we had to use the `initialDelaySeconds` parameter 
  - available for both liveness and readiness probes
- `initialDelaySeconds` is a rigid delay (always wait X before running probes)
- `startupProbe` works better when a container start time can vary a lot


## Links:
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/