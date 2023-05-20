#  Server Dry Run

## Using server-dry-run and diff
- we already talked about using `--dry-run` for building yaml
- lats talk more about options for testing yaml
- including testing against the live cluster API
  

## using `--dry-run` with `kubectl apply`
- the `--dry-ruin` option can also be used with `kubectl apply`
- however it can be misleading it does not do a real dry run
- lets see what happens in the following scenario
  - generate the yaml for a deployment
  - tweak the yaml to transform it into a DaemonSet
  - apply that yaml to see what would actually be created
  
## the limits of `kubectl apply --dry-run`

exercise
- generate the yaml for a deployment
    `kubectl create deployment web --image=nginx -o yaml > web.yaml`
- change the `kind` in the yaml for make it a `DaemonSet`
- ask `kubect` what would be applied:
  - `kubectl apply -f web.yaml --dry-run --validate=false -o yaml`

The resulting YAML: does not represent a valid DaemonSet 


## Server-side dry run

- since kubernetes 1.13 we can use server side dry run and diffs
- server-side dry run will do all the work, but not persist to etcd
- (all validation and mutation hooks will be executed)

Exercise:
- try the same yaml file as earlier with server-side dry run:
- `kubectl apply -f web.yaml --server-dry-run --validate=false -o yaml`

- update use `--dry-run=server`

The resulting YAML does not have the replicas field anymore
instead it has the fields expected in a DaemonSet


## Adventages of server-side dry run
- the yaml is verified much more extensively
- the only step that is skipped is write to etc
- YAML that passes server-side dry run should apply successfully
  - unless the cluster state changes by the time the yaml is actually applied
- validating or mutating hooks that have side effect can also be an issue



## Links
https://kubernetes.io/blog/2019/01/14/apiserver-dry-run-and-kubectl-diff/
