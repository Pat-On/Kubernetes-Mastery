# Exposing DockerCoins


## Exposing services for external access
- now we would like to access the Web UI
- we will expose it with a `NodePort`
  - just like we did for the registry

Exercise:
- Create a `NodePort` service for the web UII:
  - `kubectl expose deploy/webui --type=NodePort --port=80`

- check the port that was allocated:
  - `kubectl get svc`