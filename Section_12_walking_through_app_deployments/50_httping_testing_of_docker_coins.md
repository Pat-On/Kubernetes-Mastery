# Httping testing DockerCoins


## Why are we stuck at 10 hashes per second?
- if this was high-quiality, production code, we would have instrumentation
  - Datadog, HoneyComb, new Relic, statsd, sumologic
- it is not
- perhaps we could benchmark our web services?
  - with tools like `ab` or even simpler `httping`

## Benchmarking our web servives
- we want to check `hasher` and `rng` 
- we are going to use `httping`
- it is just like `ping` but usiong http `get` requests
  - it measures how long it takes to perform one get requests

- it is used like this
  - `httping [-c count] http://host:port/path`

- or even simpler 
  - `http ip.ad.dr.ess`

- we will use `httping` on clusterIP address of our services

## Obtaining ClusterIP adresses

- we can simply check the oputput of `kubectl get services`
- or do it programatically, as in the exampkle below:

exercise:
- retrieve the ip addresses:
  - `HASHER=$(kubectl get svc hasher -o go-template={{.spec.clusterIP}})`
  - `RNG=$(kubectl get svc rng -o go-template={{.spec.clusterIP}})`

## Checking `hasher` and `rng` response times

- remember to use `shpod` on MacOS and Windows
  - kubectl apply -f https://bret.run/shpod.yml
  - kubectl attach --namespace=shpod -ti shpod

- check the response times for both servbices
  - httping -c 3 $HASHES
  - httping -c 3 $RNG




## Lets draw hasty conclusions
- the bottleneck seems to be `rng`
- what if we do not have enough entropy and can not generate enough random numbers?
- we need to scale out the `rng` service on multiple machines

Not this is a fiction. We have tnough entropy but we need a pretext to scale out

(in fact the code of rng uses dev/urandom, which never runts out of entropy... and it just as good as dev/random)