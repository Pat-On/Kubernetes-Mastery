Kubernetes concepts

- kubernetes is a container management system
- it runs and manages containerized applications on a cluster (one or more servers)
- often this is simply called container oirchestration
- sometimes shotened to kube or k8s 


Basic things we can ask kubernetes to do:
- start 5 containers using image atseashop/api
- place an internal load balancer in front of these containers
- start 10 containers using image atseashop/webfront:v1.3
- place a public load balancer in front of these containers
- its black friday or christmas, traffic spikes, grow our cluser and add containers
- new release replace my containers with the new image atseashop/webfront:v1.4
- keep procerssing requeszts during the upgrade; update my containers one at a time


Other things that kubernetes can do for us
- basic autoscaling
- blue/green deployment, canary deployment
- long running services but also batch one-off and cron-like jobs
- overcommit our cluser and evict low-priority jobs
- run services access control defining what can be done by whom on which resources
- integrating third party servicews (service cxatalog)
- automating complex tasks (operators )