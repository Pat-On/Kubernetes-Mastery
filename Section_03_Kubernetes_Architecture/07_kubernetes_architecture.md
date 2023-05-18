https://kubernetes.io/docs/concepts/overview/components/
https://kubernetes.io/docs/concepts/architecture/nodes/


# Kubernetes Architecture

Master - control plane
- API SERVER - everything is talking through it (manage scheduler and controller)
- etcd - database key value storage, contain everything
- Scheduler
- Controller Manager


node 1
- container runtime - it is docker 
- c1/c2/c3/cx they are application
- OS <- linux machine
- Infrastructure <- virtual machine or metal
- kubelet - agent that talk back to api
- kube-proxy manage networking. it take ordsers from kubelet and issue ip addresses etc


overlay network (flannel/openVSwitch/weave)
  
coreDNS - it theoretically optional but required to run the services
