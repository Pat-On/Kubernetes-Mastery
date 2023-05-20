# Failed Update Details

## Rolling out something invalid

- what happens if we make a mistake

Exercise
- Update `worker` by specifying a non-existent image:
    kubectl set image deploy worker worker=dockercoins/worker:v0.3

- check what is going on:
    kubectl rollout status deploy worker

our rollout is stuck. However, the app is not dead
(after a minute it will stabilize to be 20-25% slower.....)

## What is going on with our rollout?
- why is our app a bit slower
- because `MaxUnavailable=25%`
- so the rollout terminated 2 replicas out of 10 available
- okey but why do we see 5 new replicas being rolled out?
- because `MaxSurge=25%`
- so in addiution to replacing 2 replicas, the rollout is also starting 3 more
- it rounded down the number of `MaxUnavailable ` pods conservatively
- but the total number of pods being rolled out is allowed to be 25+25=50%

## The nitty-gritty details
- we start with 10 pods running for the `worker` deployment
- current settings: `MaxUnavailable=25%` and `MaxSurge=25%`
- when we start the rollout:
  - two replicas are taken down (as per MaxUnavailable=25%)
  - two others are created (with the new version) to replace them
  - three others are created (with the new version) per `MaxSurge=25%`

- now we have 8 replicas up and running, and 5 being deployed
- out rollout is stuck at this point! <--- Interesting





## Links:
https://kubernetes.io/docs/tasks/debug/debug-application/determine-reason-pod-failure/
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#deployment-status