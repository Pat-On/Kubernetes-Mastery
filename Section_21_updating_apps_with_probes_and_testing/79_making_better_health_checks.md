# Making Better Healthchecks

## Discussion
- Above a given threshold the liveness probe starts failing
  - about 10 concurrent requests per backend should be plenty enough
- when the liveness probe fails 3 times in a row, the container is restarted
- during the restart there is less capacity available
- meaning that the other backends are likely to timeout as well
- eventually causing all backends to be restarted
- and each fresh backend gets restarted too
- this goes until the load goes down or we add capacity

this would not be a good healthcheck in real application :>


## Better healthchecks
- we need to make sure that the healthcheck does not trip when performance degrades due to external pressure
- using a readiness check would have fewer effects
  - but it would still be an imperfect solution
- possible combination:
  - readiness check with a short timeout / low failure threshold
  - liveness check with a longer timeout / higher failure threshold

[better solution - horizontal scaling based on the traffic! :> ]