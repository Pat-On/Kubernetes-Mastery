# Kubernetes Deploys With YAML

## Deploying with YAML

- so far we created resources with the following commands:
  - `kubectl run`
  - `kubectl create deployment`
  - `kubectl expose`

- we can also create resource directly with YAML manifests

## `kubectl apply` vs `kubectl create`
- `kubectl create -f whatever.yaml`
  - creates resources if they do not exist
  - if resources already exist do not alter them
    - and display error msg

- `kubectl apply -f whatever.yaml`
  - creates resources if they do not exist
  - if resources already exists update them
    - to match the definition provided by the yaml file
  - stores the manifest as an annotation in the resource

## creating multiple resources

### the manifest can contain multiple rezosurces separated by ---

```
kind: ...
apiVersion: ...
metadata:
    name: ...
    ...
spec:
    ...
---
kind: ...
```

### the manifest can also contain a list of resources

apiVersion: v1
kind: List
items:
- kind: ...
  apiVersion: ...
- kind: ...
  apiVersion: ...


## Deploying DockerCoins with YAML
- we provide a YAML manifest with all the resources for DockerCoins
  - deployments and services
- we can use it if we need to deploy or redeploy docker coins

Exercise: 
- deploy or redeploy DockerCoins
- `kubectl apply -f https://k8smastery.com/dockercoins.yaml`

- note  the warning if you already had the resources created
- this is because we did not use apply before
- this is ok for us learning so ignore the warnings
- generally in production you want to stick with one method or the other

