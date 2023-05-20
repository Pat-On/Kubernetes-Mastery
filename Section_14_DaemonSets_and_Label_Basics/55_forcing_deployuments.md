# Forcing Deployment into DaemonSet

## Creating the YAML file for our daemon set
- lets start with the YAML file for the current `rng` resource

exercise:
- Dump the `rng` resource in YAML:"
  - `kubectl get deploy/rng -o yaml >rng.yml`

- edit `rng.yml`



## LINKS
https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/