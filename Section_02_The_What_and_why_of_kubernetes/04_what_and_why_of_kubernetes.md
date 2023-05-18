# What and why of orchestration

- there are many computing orchestrators
- they make decisions about when and where to do work
- we have done this since the dawn of computing:
  - mainframe schedulerst- Pupper
  - terraform
  - aws
  - Mesos
  - hadoop 

- Since 2014 we have had a resurgence of new orchestration projects because:
    1. Popularity of distributed computing
    2. docker containers as a app package and isolated runtime
- We needed many servers to act like one, and run many containers
- an the container orchestrator was born

- Many open source project have been created in the last 5 years to:
  - schedule running of containers on servers
  - dispatch them across many nodes
  - monitor and react to container and server health
  - provide storage, networking, proxy, security and logging features
  - do all this in a declarative way, rather than imperative
  - provide api's to allow extensibility and management


# Major container orchestration project
- Kubernetes aka k8s
- docker swarm and swarm classic
- apache mesos / marathon
- cloud foundry
- amazon ECS (not oss, aws only)
- HashiCorp Nomad
- many of these tools run on top of docker engine
- Kubernetes is the one orchestrator with many distributions

