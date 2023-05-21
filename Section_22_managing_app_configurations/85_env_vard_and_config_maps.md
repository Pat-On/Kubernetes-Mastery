# Env Vars and Config Maps

## Environment variables, pros and cons
- works great when the running program expects these variables
- works great for optional parameters with reasonable defaults
  - since the container image can provide these defaults
- sort of auto-documented
  - we can see which env variables are defined in the image, and their values
- can be used with longer values... (abused)
  - you can put an entire Tomcat configuration file in an env...
  - .... but should you

do it if you really need to we are not judging! but we will see better ways

## Injecting configuration files with ConfigMaps
### second probably the most common ways

- sometimes there is no way around it: we need to inject a full config file
- kubernetes provides a mechanism for that purpose: `ConfigMaps`
- A ConfigMap is a K8s resource that exists in a namespace
- conceptually it is a key value map
  - values are arbitrary string
- we can think about them in (at least) two different ways:
  - as holding entire configuration file(s)
  - as holding individual configuration parameters
  
  note to hold sensitive information we can use "Secrets" which are another type of resource behaving very much like ConfigMaps.
  we will cover them just after

  ## ConfigMaps storing entire files
  - in this case, each key/value pair corresponds to a configuration file
  - key = name of the file
  - value = content of the file
  - there can be one key/value pair or as many as neccessary
    - for complex apps with multiple configuration files
  - examples|:
    - `kubectl create configmap my-app-config --from-file=app.conf`
    - `kubectl create configmap my-app-config --from-file=app.con=app-prod.conf`
    - `kubectl create configmap my-app-config --from-file=config.d/`



## ConfigMaps storing individual parameters (everything is in the Kubernetes)
- in this case, each key/value pair corresponds to a parameter
- key = name of the parameter
- value = value of the parameter
- examples:
```
# create a config map with two keys
kubectl create cm my-app-config \
    --from-literal=foreground=red \
    --from-literal=background=blue

# create a ConfigMap from a file containing key=val pairs
kubectl create cm my-app-config \
    --from-env-file=app.conf
```

