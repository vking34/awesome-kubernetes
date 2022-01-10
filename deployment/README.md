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

## Labels

- a label can be used as a key/value pair for further identification of k8s resources

- This can be useful for locating resources

- Lables are also used by k9s itself for pod selection by deployment and services
    - Deloyments are monitoring a sufficient amount of pods through the label

    - When creating services using `kubectl expose`, a label is automatically added

- Use the `selector` option to search for items that have a specific label set
```
kubectl get pods --selector='run=httpd'
```

- To label object
```
kubectl label deployment my-deployment ml=example
```

## Annotations

- Annotations are used to provide detailed metadata in an object

- Annotations can not be used in queries, they are just to provide additional information

- Think of information about license, maintainer and more

## History

- Major changes cause the deployment to create a new ReplicaSet that uses the new properties

- The old ReplicaSet is still kept, but the number of pods will be set to 0

- This makes it easy to undo a change

- `kubectl rollout history` will show the rollout history of specific deployment, which can easily be reverted as well

## Rolling Update

- It is the task of deployment to ensure that sufficient number of pods are running at all times

- So when making a change, this change is applied as rolling update: the changed version is deployed and after that has been confirmed as successful, the old version is taken offile

- You can use `kubectl rollout history` to get details about recent transactions

- Use `kubectl rollout undo` to undo a previous change

- When a Deployment changes, pods are immediately updated according to the update strategy:
    - Recreate: all pods are killed and new pods are created. This will load to temporary unavailibility (downtime). Useful if you cannot simultaneously run different versions of an app

    - RollingUpdate: updates pods one at a time to guarantee availability of the app. This the preferred approach and you can further tune its behaivor

- The RollingUpdate options are used to guarantee a certain minimal and maximal amount of pods to be always available:
    - `maxUnavailable`: determines the maximum number of pods that are upgraded at the same time

    - `maxSurge`: the number of pods that can run beyond the desired number of pods as specified in a replica to guarantee minial vailability

