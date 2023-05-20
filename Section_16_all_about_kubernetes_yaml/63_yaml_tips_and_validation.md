# YAML: Tips and Validation

## Advantage of YAML
- Using YAML instead of `kubectl run/create/etc/` allows to be declarative
- the yaml describes the desired state of our cluster and applications
- yaml can be stored, versioned, archived eg in git repositories
- to change resources change the YAML files
  - instead of using `kubectl edit/scale/label/etc`
- changes can be reviewed before being applied
  - with code reviews, pull requests...
- this workflow is sometimes called gitops
  - there are tools like Weave Flux or GitKube to facilitate it

## YAML in practice
- get started with `kubectl run/create/expose`
- dump the yaml with `kubectl get -o yaml`
- tweak that yaml and `kubectl apply` it back
- store that yaml for reference (for further deployments)
- feel free to clean up the yaml
  - remove fields you do not know
  - check that it still works
- that yaml will be useful later when using e.g. Kustomize or helm

## YAML linting and validation
- use generic linter to check proper YAML formatting
  - yamllint.com
  - codebeautify.org/yaml-validator
- for humans without kubectl, use web Kubernetes YAML validator: kubeyaml.com
- in CI you might use CLI tools
  - YAML linter: `pip install yamllint` 
  - kubernetes validator `kubeval`

- we will learn about Kubernetes cluster-specific validation with kubectl later 

