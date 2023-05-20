# Kubernetes Image Registries

## Shipping images with a registry

- for development using Docker, it has build, ship, and run features
- now that we wawant to run on a cluster things are different
- kubernetes does not have a build feature built-in
- the way to ship (pull) images to Kubernetes is to use a registry




## how docker registries work (a  reminder)
- what happens when we execute `docker run alpine`?
- if the engine needs to pull the `alpine` image it expands it into `library/alpine`
- `library/alpine` is expanded into `index.docker.io/library/alpine`
- the engine communicates with `index.docker.io` to retrieve `library/alpine:latest`
- to use something else than `index.docker.io` we specify it in the image name


Example (this is done by Kubernetes when it is using Docker in kublets)
`docker pull gcr.io/google-containers/alpine-with-bash:1.0`
`docker build -t registry.mycompany.io:5000/myimage:awesome .`
`docker push registry.mycompany.io:5000/myimage:awesome`

## Building and shipping images
- there are many options
- manually
  - build locally (with docker build or oterwise)
  - push to registry

- Automatically
  - build and test locally
  - when ready, commit and push a code repository
  - the code repository notifies and automated build system
  - that system gets the code builds it pushes the image to the registry

 
## Which registry do we want to use?
- thjere are SAAS products like Docker Hub, Quay, GitLab...
- each major cloud provider has an option as well (ACR on Azure, ECR on AWS, GCR on Google Cloud)
- there are also commercial products to run our own registry
  - Docker Enterprise DTR, Quay, GitLab,. JFrog Artifactory

- and open source option too!
  - Quay, Portus, OpenShift OCR, GitLab, Harbor, Kraken

- When picking a registry pay attention to:
  - its build system
  - multi-uiser auth and mgmt RBAC
  - storage features (replication, caching, garbage collection)


Links:
https://awesome-docker.netlify.app/#registry