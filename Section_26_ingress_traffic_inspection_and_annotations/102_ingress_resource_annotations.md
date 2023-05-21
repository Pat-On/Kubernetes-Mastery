# Ingress Resource Annotations

## Adding features to a Ingress Resource

- reverse proxies have lots of features
- lets add a 301 redirect to a new ingress resource using annotations
- it will apply when any other path is used in url that we did not already add

Exercise:
create a redirect

`kubectl apply -f https://k8smastery.com/redirect.yaml`




## Links
https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/