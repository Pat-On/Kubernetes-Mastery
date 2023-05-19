# Resource creation and run changes

## What about that deprecation warning?
- as we can see from the prveiuous slide `kubectl run` can do many things
- the exact type of resource created is not obvious
- to make this more explicit it is better to use kubectl create:
  - `kubectl create deployment` to create a deployment
  - `kubectl create job` to create a job
  - `kubectl create cronjob` to run a job periodically (since kubernetes 1.14)

- eventually `kubectl run` will be used only to start one-shot pods


## Various ways of creating resources

- `kubectl run`
  - easy way to get started
  - versatile

- `kubectl create <resource>`
  - explicit but lacks some features
  - can not create a cron job before kubernetes 1.14
  - can not pass command-line arguments to deployments

- `kubectl create -f foo.yaml` or `kubectl apply -f foo.yaml`
  - all features are available
  - requires writing YAML

