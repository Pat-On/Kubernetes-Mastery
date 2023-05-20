# DockerCoins on Kubernetes

- Create one deployument for each component
  - hasher redis rng webui worker

- expose deployments that need to accept connections
  - hasher redis rng webui
- for redis we can use the official redis image
- for the other 4 we need to build images and push them to some registry

## Using images from the Docker Hum

- for everyone's convenience we took care of building DockerCoins images
- we pushed these images to the DockerHub under the dockercoins user
- these images are tagged with a version number `v0.1`
- the full image names are therefore:
  - `dockercoins/hasher:v0.1`
  - `dockercoins/rng:v0.1`
  - `dockercoins/webui:v0.1`
  - `dockercoins/worker:v0.1`

