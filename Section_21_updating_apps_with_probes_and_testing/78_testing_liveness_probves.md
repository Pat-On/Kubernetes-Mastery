# Testing liveness probe

- The rng service needs 100ms to process a requests
   because it is single threaded and sleeps 0.1s in each requiests
- the probe timout is set to 1 seconmd
- if we send more that 10 requests per second per backend it will break
- lets generate traffic and see what happens

Exercise:
get the clusterIP address of the rng service:
    `kubectl get svc rng`

## monitoring the rng service
- each command bellow will show us what is happening on a different level

- in one window monitor cluster events
  - `kubectl get events -w`
- in another window monitor pods status
  - `kubectl get pods -w`

## Generating traffic
- lets use `ab` (apache bench) to send concurrent requests to rng

exercise: 
in yet another window, generate traffic using `shpod`:

`kubectl attach --namespace=shpod -ti shpod`
`ab -c 10 -n 1000 http://<cluserIP>/1`

experiment with higher values of `-c` and see what happens

- the `-c` parameter indicates the number of concurrent requests
- the final `/1` is important to generate actual traffic
  - otherwise we would use the ping endpoint which does not sleep 0.1 per request


## Testing the liveness probe
- the rng service needs 100ms to process a request
  - because it is single-threaded and sleeps 0.1s in each req
- the probe timeout is set to 1 second
- if we send more than 10 requests per second per backend it will break
- lets generate traffic and what happens

Get the ClusterIP address of the rng service:
    `kubectl get svc rng`


## links:
https://httpd.apache.org/docs/current/programs/ab.html