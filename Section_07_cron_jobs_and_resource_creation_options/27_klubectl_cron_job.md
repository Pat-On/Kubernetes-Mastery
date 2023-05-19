# What if we wanted something different?
- what if we wanted to start a one-shot container that does not get restarted?
- we could use `kubectl run --restart=OnFailure` or `kubectl run --restart=Never`
- these commands would create jobs or pods instead of deployments
- under the hood, kubectl run invokes 'generators' to create resource descriptions
- we could also write these resource descriptions ourselves (typically in yaml), and create them on the cluster with `kubectl apply -f` (discussed later)
- with `kubectl run --schedule=...` we can also create cronjobs

## IMPORTANT in 1.18 run only creates a pod, and no longer supports these generators 

## Scheduling periodic background work

- a cron job is a job that will be executed at specific intervals
  (the name comes from the traditional cronjobs executed by tje unix crond)
- it rquires a schedule, represented as five space-separated fields
  - minute
  - hour
  - day of the month
  - month of the year
  - day of the week [0, 6] 0 - Sunday
- * means 'all valid values /N means every N
- example: */3 * * * * means every three minutes

## from 1.18 use `kubectl create cronjob`

`kubectl create cronjob my-job --schedule="*/3 * * * *" --restart=OnFailure --image=alpine`

`kubectl create cronjob every3mins --image alpine --schedule="*/3 * * * *" --restart=OnFailure -- sleep 10`

`kubectl get cronjobs`

## Cron Jobs in action

- at the specified schedule, the cron job will create a job
- the job will create a pod
- the job will make sure that the pod completes
  - recreating another one if it fail, for instance if its node fail

`kubectl get jobs`

