# YAML PATCH

## Changing rollout parameters

- what if we wanted to all at one
  - change image to v0.1
  - be conservative on availability (always have desired number of available worker)
  - go slow on rollout speed (update only one pod at a time)
  - give some time to our workers to 'warm up' before starting more

The corresponding changes can be expressed in the following YAML snippet:

```
spec:
    template:
        spec:
            containers:
            - name: worker
              image: dockercoins/worker:v0.1
    strategy:
        rollingUpdate:
            maxUnavailable: 0
            maxSurge: 1
        minReadySeconds: 10

```

## applying changes through a YAML patch
- we could use kubectl edit deployment worker
- but we could also use `kubctl patch` with the exact YAML shown before

