# Jobs

- Pod normally are created to run forever

- To create a pod that runs for a limited duration, use __jobs__ instead

- Jobs are useful for tasks, like backup, calculation, batch processing and more

- A pod that is started by __a job must have__ its `restartPolicy` set to `OnFailure` or `Never`
    - `OnFailure` will re-run the container on the same pod

    - `Never` will re-run the failing container in a new pod


## Types

- 3 types are specified by the __completions__ and __parallelism__ parameters:

    - Non-parallel jobs: one pod is started, unless the pod fails
        - `completions=1`
        - `parallelism=1`

    - Parallel jobs with a fixed completion count: the job is complete after successfully running as many times as specified in jobs.spec.completions
        - `completions=n`
        - `parallelism=m`

    - Parallel jobs with a work queue: multiple jobs are started, when one completes successfully, the job is complete
        - `completions=1`
        - `parallelism=n`
    
## Cronjobs

- jobs are used to run a task a specific number of times

- Cronjobs are used for tasks that need to run on a regular basis

- When running a Cronjob, a job will be scheduled

- This job, on its turn, will start a pod


```
kubectl get cronjobs.batch

kubectl delete cronjobs.batch cronjob-name
```