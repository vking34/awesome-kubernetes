# K8S management interfaces

![k8s-management-interfaces](../assets/images/k8s-management-interfaces.png)

- __API__:
    - is RESTful
    - receives commands, configuration from:
        - __kubectl__
        - __Dashboard__
        - __curl__

    - defines objects in a k8s environment

- __ectd__: a configuration DB


## Authentication & Authorization

- Authentication is about whre k8s users come from

- `kubectl` config specifies to which cluster to authenticate (using `kubectl config view`)

- Authorization is what these users can do

- Behind authorization, there is RBAC to take care of the different options

- Use `kubectl auth can-i` ...  to find out what you can do