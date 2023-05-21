# Probe types and examples

## benefits of using probes

- rolling updates proceed when containers are actually ready
  - are opposed to merely started
- Containers in a broken state get killed and restarted
  - instead of serving errors or timeouts
- Unavailable backends get removed from load balancer rotation
  - this improving response times across the board
- if a probe is not defined, it is as if there was an alays successful probe\


## Different types of probe handlers
- HTTP request
  - specify URL of the request (and optional headers)
  - any status code between 200 and 399 indicates success

- TCP connection
  - the probe succeeds if the TCP port is open

- arbitrary exec (the most expensive - use more resources)
  - a command is executed in the container
  - exit status of zero indicates success

## Timing and thresholds
- probes are executed at intervals of `periodSeconds` (default: 10)
- the timeout for a probe is set with `timeoutSeconds` (default: 1)

if a probe takes longer than that it is considered as a fail

- a probe is considered successful after `successThreshold` successes (default: 1)
- a probe is considered failing after `failureThreshold` failures (default: 3)
- a probe can have a `initialDelaySeconds` parameter (default: 0)
- Kubernetes will wait that amount of time before running the probe for the first timer
  - this is important to avoid killing services that take a long time to start 

## Example: HTTP probe
- here is a pod template for the `rng` web service of DockerCoins app:
```
apiVersion: v1
kind: Pod
metadata:
    name: rng-with-liveness
spec:
    containers:
    - name: rng
      image: dockercoins/rng:v01
      livenessProbe:
        httpGet:
            path: /
            port: 80
        initialDelaySeconds  # maybe startup seconds in newer versions
        periodSeconds: 1   # pretty aggresive
```


## Example: exec probe

Here is a pod template for a Redis server:

```
apiVersion: v1
kind: Pod
metadata
    name: redis-with-liveness
spec:
    containers:
    - name: redis
      image: redis
      livenessProbe:
          exec:
            command: ['redis-cli', 'ping']

```

If the redis process becomes unresponsive, it will be killed

