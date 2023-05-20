# our sample microservice app

## What is this application?
- it is a DockerCoin miner?
- no you can not buy coffee with dockercoin
- how docker coins works
  - generate a few random bytes
  - hash these bytes
  - increment a counter (to keep track of speed)
  - repeat forever
- DockerCoins is not a cryptocurenncy
  - the only common points are randomness hashing and coins in the name


## Dockercoins in the microservices era

- DockerCoins is made of 5 services:
  - `rng` - web service generating random bytes
  - `hasher` - web service computing hash of POSTed data
  - `worker` background process calling rng and hasher
  - `webui` - web interface to watch progress
  - `redis` - data store hgold a counter updated by worker

- these 5 services are visible in the application's compose file


## service discovery in container-land

### how does each service find out the address of the other ones?
- we do not hard-code IP addresses in the code
- we do not hard-code FQDNs in the code, either
- We just connect to a service name, and container-magic does the rest
    and by container-magic we mean a crafty, dynamic, embedded DNS server


## DockerCoins at work
- `worker` will log HTTP request to `rng` and `hasher`
- `rng` and `hasher` will log incoming HTTP requests
- `webui` will give us a graph on coins mined per second

Links:
https://github.com/BretFisher/kubernetes-mastery/tree/mastery/dockercoins
https://slides.kubernetesmastery.com/images/dockercoins-diagram.svg