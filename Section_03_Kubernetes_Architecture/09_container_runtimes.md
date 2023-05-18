# Containers Runtime

Do we need to run Docker at all?
- by default, kubernetes uses the docker engine to run containers
- or leverage other pluggable runtimes through the container runtime interface
- we could also use rkt rocket from coreos <---- deprecated
- containerd: maintained by docker, ibm and community
- used by docker engine, microk8s k3s gke and standalone has ctr CLI
- CRI-O maintained by Red Hat, SUSE and community based on containerd
- used by openshift and kubic, version matched to kubernetes


Do we need to run docker at all?
Yes!
- in this course we will run our apps on a single node first
- we may need to build images and ship them around
- we can do these things without docker (and get diagnosed with NIH syndrome)
- Docker is still the most stable container engine today (but other options are maturing very quickly)

NIH - Not Invented Here

# Do we need to run docker at all/
- on our dvelopment env, ci pipeline
  - yes almost certainly
- on your production servers
  - yes (today)
  - probably not (in the future)

### links

https://kubernetes.io/blog/2016/12/container-runtime-interface-cri-in-kubernetes/
https://github.com/cri-o/cri-o/blob/main/README.md
https://github.com/containerd/containerd/blob/main/README.md
https://kubernetes.io/docs/setup/production-environment/container-runtimes/