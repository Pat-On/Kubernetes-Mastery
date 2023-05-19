# Accessing logs from the CLI

- the`kubectl logs` command has limitations:
  - it cannot stream logs from multiple pods at a time
  - when showing logs from multiple pods it mixes them all together

- we are going to see how to do it better

## Doing it manually
- We could (if we were so inclined) write a program or script that would
  - take a selector as an argument
  - enumerate all pods matching that selector with `kubectl  get -l ...`
  - fork one `kubectl logs --follow ...` command per container
  - annotate the logs (the output of each `kubectl logs....` process) with their origin
  - preserver ordering by using `kubectl logs --timestamps ...` and merge the output 

## Stern
- stern is an open source project by Wercker
- From the Reamde:
- stern allows you tyo tail multiple pods on Kubernetes and multiuple containers within the pod
- each result is color coded for quick debugging

- the query is a regular expression so the pod name can easily be filtered an you do not need to specify the exact id (for instance omitting the deployment id).
- if a pod is deleted it gets removed from tail and if a new pod is added it automatically gets tailed.

- exactly what we need

## installing stern

- Run stern without arguments to check it is its installed
- go and check documentation

## Using stern
- there are two ways to specify the pods whose logs we want to see:
  - `-l` followed by a selector expression (like with many `kubectl` commands)
  - with a pod query ie a regex used to match pod names

- these two ways can be combined if eneccessary

stern pingpong