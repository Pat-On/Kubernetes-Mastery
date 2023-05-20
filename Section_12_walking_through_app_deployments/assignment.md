# What deployment commands did you use to create the pods?

kubectl create deployment db --image=bretfisher/wordsmith-db
kubectl create deployment web --image=bretfisher/wordsmith-web
kubectl create deployment api --image=bretfisher/wordsmith-api
# What service commands did you use to make the pods available on a friendly DNS name?

kubectl expose deployment db --port=5432
kubectl expose deployment web --port=80 --type=NodePort
kubectl expose deployment api --port=8080
or this will also work:

kubectl create service clusterip db --tcp=5432
kubectl create service nodeport web --tcp=80
kubectl create service clusterip api --tcp=8080
Then you'll want to get the port that web is listening on the host:

kubectl get service web

# What if we needed to add more wordsmith-api pods. What is the command to scale that deployment up to 5 pods?

kubectl scale deployment api --replicas=5