## Kubernetes Architecture

![](../assets/images/k8s-architecture.png)

- k8s is running in a cluster having 1 master node (controller node) and mutiple minion nodes (worker nodes)

- Master node:
    - is like a brain of k8s

    - __kube-apiserver__: where k8s management client talk to

    - __kube-scheduler__: is the part that pushes the workload to a specific worker node

    - __etc__: is a key-value DB that store configurations
    
    - __kube-controller-manager__: control the processes

- Minion node:
    - __kubelet__: receive workload from kube-scheduler

    - __kube-proxy__: used in communication to make sure that secure end-to-end communication can happen through REST by API server and worker nodes