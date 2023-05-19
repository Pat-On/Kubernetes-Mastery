# deleting pods and watching

## streaming logs of multiple pods

- what happens if we restart `kubectl logs`?

exercise:
- interrupt `kubectl logs` with ctrl-c
- restart it
  - `kubectl logs deploy/pingpong --tail 1 --follow

`kubectl logs` will warn us that multiple pods were found, and that its showing us only one of them

Lets leave `kubectl logs` running while we keep exploring


## what happened?
- `kubectl delete pod` terminates the pod gracefully
  (sending in the TERM signal and waiting for it to shut down)
- as soon asthe pod is in "terminating" state, the replica set replaces it
- but we can still see the output opf the terminating pod in `kubectl logs`
- until 30 second later when the grace period expires
- the pod is then killed and `kubectl logs` exits

