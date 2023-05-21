# Deploying NGINX Ingress

## Running NGINX on our cluster
- now lets deploy the NGINX controller. Pick your distro:

- apply the YAML
  - for Docker Desktop
  - `kubectl apply -f https://k8smastery.com/ic-nginx-lb.yaml`

  - fir minikube/MicroK8s
  - `kubectl apply -f https://k8smastery.com/ic-nginx-hn.yaml`

- check the pod status
    `kubectl describe -n ingress-nginx deploy/nginx-ingress-controller`


## deploying the nginx ingress controller
the two main section in the yaml are:

- nginx deployment (or DaemonSet) and all its required resources
  - namespace
  - ConfigMaps (storing NGINX configs) - it is letting NGINX communicate with K8s
  - ServiceAccounts (authenticate to Kubernetes API)
  - Role/ClusterRole/RoleBindings (Authorization to API ports)
  - LimitRange (limit cpi/memory of nginx)
- Service to expose NGINX on 80/443
  - different for each Kubernetes distribution

```
NAME                                            READY   STATUS    RESTARTS   AGE
pod/ingress-nginx-controller-5457fbc8bf-fzzbp   1/1     Running   0          6m59s

NAME                               TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/ingress-nginx-controller   LoadBalancer   10.108.91.170   localhost     80:30928/TCP,443:31640/TCP   6m59s

NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/ingress-nginx-controller   1/1     1            1           6m59s

NAME                                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/ingress-nginx-controller-5457fbc8bf   1         1         1       6m59s
```


## to get all created resources

`kubectl get all -n ingress-nginx`

---

## checking that nginx runs correctly
- if nginx started correctly we now have a web server listening on each node
- direct your browser to your k8s IP on port 870
- we should get a 404 page not found error
- this is normal because we have not provided any rules for ingress


## Links:
https://slides.kubernetesmastery.com/#652
https://kubernetes.github.io/ingress-nginx/deploy/
https://github.com/kubernetes/ingress-nginx
https://slides.kubernetesmastery.com/#677