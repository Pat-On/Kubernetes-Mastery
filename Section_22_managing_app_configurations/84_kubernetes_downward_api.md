# Kubernetes Downward API 


## The Downward API
- in the previous example, environment variables have fixed values
- we can also use a machanism called the Downward API
- the downward API allows exposing pod or container information
  - either through special files (we won't show that for now)
  - or through env variables
- the value of these env variables is computed when the container is started
- remember: env variables won't (can not) change after container start
- lets see a few concrete examples!


## Exposing the pod's namespace

```
- name: MY_POD_NAMESPACE
  valueFrom
    fieldRef:
      fieldPath: metadata.namespace
```

- Useful to generate FQDN of services
  - in some contexts a short name is not enough
- for instance the two commands should be equivalent

`curl api-backend`
`curl api-backend.$MY_POD_NAMESPACE.svc.cluster.local`

## exposing the pod's IP address
```
- name: MY_POD_IP
  valueFrom:
    fieldRef:
       fieldPath: status.podIP  <--- this is shared by other containers
```

- useful if we need to know our IP address
  - we could also read it from `eth0` but this is more solid

## Exposing the container's resource limits

```
- name: MY_MEM_LIMIT
  valueFrom:
    resourceFieldRef:
        containerName: test-container
        resource: limits.memory
```

- useful for runtimes where memory is garbage collected
- example: the JVM
  - the memory available to the JVM should be set with the `-Xmx` flag
- Best practice: set a memory limit, and pass it to the runtime
- note: recent versions of the JVM can do this automatically
  - see JDK-8146115 FOR DETAILS


## More about the Downward API
- check the links


## Links:
https://kubernetes.io/docs/tasks/inject-data-application/downward-api-volume-expose-pod-information/
https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/