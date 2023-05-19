# Exploring types and definitions

- we can list all available resources types by running `kubectl api-resources`
  (in kuberentes 1.10 and prior this command used to be `kubectl get`)
- we can view the definition for a resource type with:
  - `kubectl explain type`
- we can view the definition of a field in a resource for, instance:
  - `kubectl explain node.spec`
- or get the list of all fields and sub-fields
  - `kubectl explain node --recursive`


# introspection vs. documentation

- we can access the same information by reading the api documentation
- the api documentation is usually easier to read but:
  - it wont show custom types (like custom resource definitions)
  - we need to make sure that we look at the correct version
- `kubectl api-resources` and `kubectl explain` perform introspection (they communicate with the API server and obtain the exact type definitions)


# type names
- the most common resource names have three forms:
  - singular (eg node, service, deployment)
  - plural (nodes, services, deployments)
  - short (n, svc, deploy)
- some resources do not have a short name
- endpoints only have a plural form
    (because even a single `Endpoints` resource is actually a list of endpoints)

https://v1-25.docs.kubernetes.io/docs/home/