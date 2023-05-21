# Inspecting Ingress Resources


## View Ingress Resources
- lets inspect some Ingress resources

Exercise:

- list all ingress resources in the default namespace

`kubectl get ingress`

```
NAME          CLASS                  HOSTS                          ADDRESS     PORTS   AGE
cheddar       cluster-wide-ingress   cheddar.127.0.0.1.nip.io       localhost   80      22m
my-google     cluster-wide-ingress   *                              localhost   80      6m55s
stilton       cluster-wide-ingress   stilton.127.0.0.1.nip.io       localhost   80      22m
wensleydale   cluster-wide-ingress   wensleydale.127.0.0.1.nip.io   localhost   80      22m

```

- get the details on the cheddar ingress resource

`kubectl describe ingress cheddar`

```
Name:             cheddar
Labels:           <none>
Namespace:        default
Address:          localhost
Ingress Class:    cluster-wide-ingress
Default backend:  <default>
Rules:
  Host                      Path  Backends
  ----                      ----  --------
  cheddar.127.0.0.1.nip.io  
                            /   cheddar:80 (10.1.1.24:80)
Annotations:                <none>
Events:
  Type    Reason  Age                From                      Message
  ----    ------  ----               ----                      -------
  Normal  Sync    22m (x2 over 22m)  nginx-ingress-controller  Scheduled for sync

```

- get the details on the my-google ingress resource

`kubectl describe ingress my-google`

```
Name:             my-google
Labels:           <none>
Namespace:        default
Address:          localhost
Ingress Class:    cluster-wide-ingress
Default backend:  <default>
Rules:
  Host        Path  Backends
  ----        ----  --------
  *           
              /   doesntmatter:80 (<error: endpoints "doesntmatter" not found>)
Annotations:  nginx.ingress.kubernetes.io/permanent-redirect: https://www.google.com
Events:
  Type    Reason  Age                    From                      Message
  ----    ------  ----                   ----                      -------
  Normal  Sync    7m29s (x2 over 7m34s)  nginx-ingress-controller  Scheduled for sync

```

- Output `stilton` in YAML

`kubectl get ingress/stilton -o yaml`

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"networking.k8s.io/v1","kind":"Ingress","metadata":{"annotations":{},"name":"stilton","namespace":"default"},"spec":{"rules":[{"host":"stilton.127.0.0.1.nip.io","http":{"paths":[{"backend":{"service":{"name":"stilton","port":{"number":80}}},"path":"/","pathType":"Prefix"}]}}]}}
  creationTimestamp: "2023-05-21T15:18:55Z"
  generation: 1
  name: stilton
  namespace: default
  resourceVersion: "128901"
  uid: f5a1f203-42ac-4458-8034-01a4e012c78d
spec:
  ingressClassName: cluster-wide-ingress
  rules:
  - host: stilton.127.0.0.1.nip.io
    http:
      paths:
      - backend:
          service:
            name: stilton
            port:
              number: 80
        path: /
        pathType: Prefix
status:
  loadBalancer:
    ingress:
    - hostname: localhost


```