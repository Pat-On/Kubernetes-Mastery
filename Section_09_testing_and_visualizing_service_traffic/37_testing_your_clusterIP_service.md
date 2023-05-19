# Testing our cluster IP service

## Testing our service

- we will now send a few http requests to our pods

- run schpod is not on linux host so we can access internal ClusterIP
  - `kubectl apply -f http://bret.run/shpod.yml`
  - `kubectl attach --namespace=shpod -ti shpod`

- lets obtain the IP address that was allocated for our service:
  - `IP=$(kubectl get svc httpenv -o go-template --template '{{ .spec.clusterIP }}')`

- send a few requests
  - `curl http://$IP:8888/`

- To much output? filter it with `jq`
  - `curl -s http://$IP:8888/ | jq .HOSTNAME`