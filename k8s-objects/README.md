# K8S Objects

- __Pod__: the basic unit in k8s; represents a set of containers that share common resources, such as an IP address and persistent volumes

- __Deployment__: standard entity that is rolled out with k8s

- __Service__: make deployments accessible from the outside by providing a single IP/port combination. Services by default provide access to pods in round-robin fashion using a load balancer

- __Ingress__: publish easy external access to services

- __Persisten Volumes (PV)__: persistent (networked) storage that can be mounted within a container by using a __Persistent Volume Claim (PVC)__
