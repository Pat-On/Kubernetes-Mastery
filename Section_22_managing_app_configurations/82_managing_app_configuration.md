# Managing App Configuration

- Some applications need to be configured
- there are many ways for our code to pick up configuration:
  - command-line arguments
  - env variables
  - configuration files
  - configuration servers
  - ... and more
- how can we do these things with containers and K8s


## Passing configuration to containers
- there are many ways to pass configuration to code running in a container:
  - baking it into a custom image
  - command-line arguments
  - env variables
  - injecting config files
  - exposing it over the k8s api
  - configuration servers
- lets review these different strategies

