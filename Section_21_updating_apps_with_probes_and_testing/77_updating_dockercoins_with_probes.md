# Updating DockerCoin Probes

## Retrieving DockerCoins manifests
- i have split up the previous `dockercoins.yaml` into one-resource-per-file
- this works with the apply commands and is easier for human to manage
- clone them locally so we can add healthcheck and re-apply


## A simple HTTP liveness probe
- this is what our liveness probe should look like:
```
containers
- name:...
image: ...
livenessProbe:
    httpGet:
        path: /
        port: 80
    initialDelaySeconds: 30
    periodSeconds: 5
```

- this will give 30 seconds to the service to start. (way more than necessary!)
- it will run the probe every 5 seconds
- it will use the default timeout (1 second)
- it will use the default failure threshold (3 failed attempts = dead)
- it will use the default success threshold (1 successful atempt = alive)



## adding the liveness probe
- lets add the liveness probe, then deploy DockerCoins
- Remember if you do not have DockerCoins running,  this will create
- if you already have DockerCoins running this will update `rng`

exercise:
- edit `rng-deployment.yaml`

load the YAML for all the resources of DockerCoins
- `kubectl apply -f`



## Links:
https://github.com/BretFisher/kubercoins