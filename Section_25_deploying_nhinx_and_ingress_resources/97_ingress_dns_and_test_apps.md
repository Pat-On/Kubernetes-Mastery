# Ingress DNA and Test Apps


## Setting up DNS 
- to make our lives easier we will use nip.io
- check out `http://cheddar.A.B.C.D.nip.io` (127.0.0.1)
  - replacing A.B.C.D with the ip address of your Kubernetes IP
- we should get the same 404 page not found error
  - meaning that our dns is set up properly so to speak


## setting up host-based routing ingress rule
- we are going to use `errm/cheese` images
  - thjere are 3 tags available:
    - wensleydale
    - cheddar
    - stilton
- These images contain a simple static HTTP server sending a picture of cheese
- we will run 3 deployments 
- We will create 3 services
- Then we will create 3 ingress rules

- We will route `<name-of-cheese>.A.B.C.D.nip.io` to the corresponding deployment

## Running cheesy web servers

- Run all three deployments

kubectl create deployment cheddar --image=errm/cheese:cheddar
kubectl create deployment stilton --image=errm/cheese:stilton
kubectl create deployment wensleydale --image=errm/cheese:wensleydale

- Create a service for each of them

kubectl expose deployment cheddar --port=80
kubectl expose deployment stilton --port=80
kubectl expose deployment wensleydale --port=80

