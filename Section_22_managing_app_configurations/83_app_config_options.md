# App Config Options

## Baking custom images
- put the configuration in the image
  - it can be in a configuration file, but also `ENV` or `CMD` options
- it is easy! it is simple
- unfortunately, it also has downsides
  - multiplication of images
  - different images for dev, staging, prod..
  - minor reconfigurations requires a whole build/push/pull cycle
- Avoid doing it unless you do not have the time to figure out other options

## Command-line arguments
- pass options to `args` array in the container specification
- example 
```
args
    - "--data-dir=/var/lib/etcd"
    - "--advertise-client-urls=http://12.0.0.1:2379"
    - "--listen-client-urls=http://127.0.0.1:2379"
    - "--listen-peer-urls=http://127.0.0.1:2380"
    - "--name=etcd"
```

- the options can be passed directly to the program that we run...
- or to a wrapper script that will use them to e.g. generate a config file

## Command-line arguments, pros & cons
- works great when options are passed directly to the running program
  - otherwise a wrapper script can work around the issue
- works great when there are not to many parameters
  - to avoid a 20 lines `args` array
- Requires documentation and/or understanding of the underlying program
  - which parameters and flags do i need, again?
- well-suited for mandatory parameters (without default values)
- not ideal when we need to pass a real configuration file anyway


## Environment variables
- pass options through the `env` map in the container specification
- example:
  
```
env:
- name: ADMIN_PORT
  value: "8080"
- name: ADMIN_AUTH
  value: Basic
- name: ADMIN_CRED
  value: "admin:0pensesame!"
```

! `value` must be a string! Make sure that numbers and fancy strings are quoted
Why this weird `{name: xxx, value: yyy}` scheme? It will be revealed soon! 

## 