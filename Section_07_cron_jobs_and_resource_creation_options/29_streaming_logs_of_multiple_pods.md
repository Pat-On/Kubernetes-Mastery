# Streaming logs of multiple pods
- can we stream the logs of all our `pingpong` pods?

exercise
- combine `-l` and `-f` flags:
  - `kubectl logs -l run=pingpong --tail 1 -f`

note: combining `-l` and `-f` is only possible since Kubernetes 1.14~


  maximum allowed concurency is 5
  use --max-log


## Why can not we stream the logs of many pods?
- `kubectl` opens one connection to the API server per pod
- for each pod, the API server opens one extra connection to the corresponding kubelet
- if there are 1000 pods in our deployment, that is 100 inbound and 1000 outbound connection the api server
- this could easily put a lot of stress on the API server
- prior kubernetes 1.14 it was decided to no allow multiple connections
- from Kubernetes 1.14 it is allowed but limited to 5 connections (this can be changed with `--max-log-requests`)
- for more details about the rationale see link bellow 



note: API is making connection to kubelet so if you would observer 1000 kublet you would have one connection to and ~~from~~

## Shortcomings of `kubectl logs`

- we do not see which pod sent which log line
- if pods are restarted / replaced the log stream stops
- if new pods are added we do not see their logs
- to stream the logs of multiple pods we need to write a selector
- there are external tools to address there shortcomings (e.g. stern)


- https://kubernetes.io/docs/concepts/cluster-administration/logging/
- https://github.com/kubernetes/kubernetes/pull/67573