# YAML Manifest


## Overview

- The recommended way to work with kubectl is by writing your manifest files and applying to manage objects in the cluster

- This declarative methodology is giving much more control than the imperative methodology where create all from CLI

- The major challenge is how to easily generate YAML files


## Ingredients

- __apiVersion__: specifics which version of the API to user for this object

- __kind__: indicate the type of object (deployment, pod, ...)

- __metadata__: contains administrative information about the object

- __spec__: contains the specifics for the object

## Commands

- `create`, `repleace`, `patch`: (imperative) tell k8s API what you want to do

- `apply`: (declarative) create objects if dont exist, update if they exist

## Tips

- Use `kubectl explain` to get more info about the basic properties

- Generate:
    - Get current state of an object: `kubectl get deployments nginx -o yaml > nginx.yaml`

    - Access the documentation at `kubernetes.io/docs`

 