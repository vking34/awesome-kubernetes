# Deployment

- When running pods in a datacenter, additional features may be needed:

    - Scalability
    - Updates and Update Strategy
    - ...

- These features are offered by `Deployments`

- `kubectl run` command was used to create deployments


## Deployemt Spec

- `replicas`: how many copies of each pod should be running

- `strategy`: how pods should be updated

- `selector`: uses `matchLabels` to identitfy how labels are matched against the pod

- `template`: contains the pod specification and is used in a deployment to create pods

## ReplicaSets

- ReplicaSet objects can be used to manage scalability from outside a deployment

- From inside a deployment, the `spec.replicas` param is used to indicate the number of desired replicas

- In current k8s, u will get a ReplicaSet when creating the deployment

- Dont manage scalability through ReplicaSets, the replicas param will take care of scalability while creating a deployment.

- Scale the number of running replicas:
```
kubectl scale deployment my-deployment --replicas=4

kubectl edit deployment my-deployment
```

