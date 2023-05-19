# viewing details
- we can use `kubectl get -o yaml` to see all available details
- however, yaml output is often simultaneously too much and no enough
- for instance, `kubectl get node node1 -o yaml` is:
  - to much infromation (e.g list of images available on this node)
  - not enough information (e.g.: does not show pods running on this node)
  - difficult to read for a human operator

- for a comprehensive overview, we can use `kubectl describe` instead

# kubectl describe
- `kubectl describe` needs a resource type and (optionally) a resource name
- it is possible to provide a resource name prefix (all maching objects will be displayed)
- `kubectl describe` will retrieve some extra information about the resource

`kubectl describe node/<node>`
`kubectl describe node <node>`

