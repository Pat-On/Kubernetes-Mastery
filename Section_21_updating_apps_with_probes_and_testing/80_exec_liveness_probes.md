# Exec Liveness Probe

## Healthcheck for redis
- a liveness probe is enough
  - it is not useful to remove a backend from rotation when it is the only one
- We could use an exec probe running `redis-cli ping`

## Exec probes and zombies
- when using exec probes we should make sure that we have a zombie reaper
- when a process terminates, its parent must call`wait()` / `waitpid()`
  - this is how the parent process retrieves the childs exit status
- in the meantime, the process is in zombie state
  - the process state will show as `Z` in `ps`, `top`
- when a process is killed its children are orphaned and attached to PID `
- PID 1 has the responsibility of reaping these processes when they terminate 
- ok but how does that affect us?

## PID 1 in containers 
- on ordinary system PID 1 (`/sbin/init`) has logic to reap processes
- in containers, PID 1 is typically our application process
  - Apache, the JVM, NGINX, Redis..
- these do not take care of reaping orphans
- if we use exec probes we need to add a process reaper
- we can add `tini` to our images
- or share the PID namespace between containers of a pod
  - and have gcr.io/pause take care of the reaping
- check the youtube link


## TINI and redis ping in a liveness probe

1. add tini to your own custom redis image
2. change the kubercoins YAML to use your own image
3. Create a liveness probe in kubercoins yaml
4. use `exec` handler and tun `tini -s -- redis-cli ping`
5. example repo here : https://github.com/BretFisher/redis-tini

```
containers:
- name: redis
  image: custom-redis-image
  livenessProbe:
    exec:
        command:
        - /tini
        - -s
        - --
        - redis-cli
        - ping
    initialDelaySeconds: 30
    periodSeconds: 5
```
[tini is the program that is going to run through docker as a additional process on redis DB]

## Links:

https://github.com/BretFisher/redis-tini
https://github.com/docker-library/healthcheck
https://www.youtube.com/watch?v=QKI-JRs2RIE&t=1431s
https://github.com/krallin/tini
https://kubernetes.io/docs/tasks/configure-pod-container/share-process-namespace/