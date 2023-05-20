# Kubernetes Dashboard

## The kubernetes Dashboard
- Kubernetes resources can also be viewed with and official web ui
- that dashboard is usually exposed over https
  - this requires obtaining a proper TLS cert
- Dashboard users need to authenticate
- we are going to take a dangerous shortcut
  
## The insecure mthod
- we could and should use lets encrypt
- but we do not want to deal with tls cert
- we could and should learn how authentication and authorization work...
- but we will use a quest account with admin access instead

## Running a Very insecure dashboard
- we are going to deploy that dasahboard with one single command
- thios command will create all the necessary resources
  - the dashboard itself the http wrapper, the admin/quest account
- all these resources are defined in a yaml file
- all we have to do is load the yaml file with kubectl apply -f


Exercvise:
`kubectl apply -f https://k8smastery.com/insecure-dashboard.yaml`



kubectl get svc 
#### Links:
https://codeberg.org/hjacobs/kube-web-view
https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
https://github.com/kubernetes/dashboard
