# Pod

- A Pod is an abstraction of a server

- It can run multiple containers within a single NameSpace, exposed by a single IP address

- k8s manage pods, not containers

- Typically, pods are only started through a deployment, because naked pods are not rescheduled in case of node failure

