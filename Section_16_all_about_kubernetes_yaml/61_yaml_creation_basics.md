# YAML creation basics


## authoring YAML
- to use Kubernetes is to live in YAML
- it is more important to learn the foundation then to memorize all YAML keys (hundreds+)

        - kubectl run
        - kubectl create deployment / kubectl create variants
        - kubectl expose
  
  - These commands use generators because the API only accepts YAML (actually JSON)
  - PRO - they are easy to use
  - CON - they have limits
  - When and why do we need to write our own YAML?
  - how do we write YAML from scratch?
  - and maybe, what is YAML?


## YAML Basics (just in case you need a refresher)
- its technically a superset of JSON designed for humans
- JSON was good for machines but not for humans
- spaces set the structure. one space off and game over
- remember spaces not tagbs EVER
- two spaces is standard, but fours spaces works too
- you do not have to learn all YAML features, but key concepts you need:
  - key/value pairs
  - array/lists
  - dictionary/maps

## Basic pats of any kubernetes resource manifest

- can be in YAML or JSON but YAML is 100
- Each file contains one or more manifests
- each manifests describes an API objects (deployment, service etc)
- each manifest needs four parts (root key: values in the files)

apiVersion
kind:
metadata:
spec:


## a simple pod in yaml
    - this is a single manifest that creates one Pod

apiVersion: v1
kind: Pod
metadata:
    name: nginx
spec: 
    containers:
    - name: nginx
    - image: nginx:1.17.3


## The limits of generated YAML
- Advanced (and even not so advances) features requirew us to write YAML:
  - pods with multiple containers
  - resource limits
  - healthchecks
  - many other resource options

- other resource types do not have their own commands!
  - DaemonSets
  - StatefulSets
  - and more!

- How do we access these features?

## we dop not have to start from scratch
- output YAML from existing resources
  - create a resource (e.g. Deployments)
  - Dump its YAML with `kubectl get -o yaml ...`
  - edit the yamls
  - use `kubectl apply -f ...` with the yaml file to:
    - update the resource (it it is the same kind)
    - create a new resource (if it is a different kind)

- or.... we have the docs with good starter YAML
  - statefulSet, DaemonSet,. ConfigMap and a ton more on Github

- or we can use `-o yaml --dry-run`


## Generating YAML without creating resources

- we can use the -o yaml --dry-run option combo with run and create

exercise:
- generate the yaml for a deployment without creating it
    - `kubectl create deployment web --image nginx -o yaml --dry-run`

- Generate the yaml for a namespace without creating it
    - `kubectl create namespace awesome-app -o yaml --dry-run`

- We can clean up the YAML even more if we want
  - for instance we can remove the `creationTimestamp` and empty dicts

## LINKS:
https://www.youtube.com/watch?v=cdLNKUoMc6c
https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html
https://developer.ibm.com/tutorials/yaml-basics-and-usage-in-kubernetes/
https://www.tutorialspoint.com/yaml/index.htm