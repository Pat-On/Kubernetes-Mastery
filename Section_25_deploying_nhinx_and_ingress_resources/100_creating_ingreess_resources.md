# Creating Ingress Resources

- Run all three deployments

kubectl create deployment cheddar --image=bretfisher/cheese:cheddar
kubectl create deployment stilton --image=bretfisher/cheese:stilton
kubectl create deployment wensleydale --image=bretfisher/cheese:wensleydale

- Create a service for each of them

kubectl expose deployment cheddar --port=80 &&
kubectl expose deployment stilton --port=80 &&
kubectl expose deployment wensleydale --port=80 &&


## Creating our first ingress resources

Exercise:
- download our YAML `curl -O https://k8smastery.com/ingress.yaml`
- edit the file `ingress.yaml` which has three ingress resources
- replace the A.B.C.D with your Kubernetes IP (127.0.0.1)
- Apply the file `kubectl apply -f ingress.yaml`
- open  http://cheddar.A.B.C.D.nip.io

an image of a piece of cheese should show up