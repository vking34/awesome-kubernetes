# Container

- A container is a self-contained ready-to-run application

- The container runtime is running on a host platform and establishes communication between the local host kernel and the container

- All containers run on top of the same local host kernel
    - Kernel is delivering access to the hardware

// TODO: Container components

- Linux Kernel Namespaces provide strict isolation between system components at different levels

    - network
    - file
    - users
    - processes
    - IPCs

- Linux Cgroups offer resource allocation and limitation

## Container Runtime

- The container rentime allows for starting running the container on top of the host OS

- The container runtime is responsible for all parts of running the container which are not already a part of the running container program itself

- Different container runtime solutions exist:
    - Docker
    - Lxc
    - Runc
    - Crio
    - Rkt

## OCI (Open Container Initative)

- It standardizes the use of containers

    - the image-spec defines how to package a container in a filesystem bundle
    - the runtime-spec defines how to run that filesystem in a container

- OCI standardization ensures compatibility between containers, no matter which environment they originally com from

## Container Components

- __image__: read-only environments that contain the runtime environment which includes the application and all libraries it requires

- __registry__: usede to store image


## Container Logging

- Logs by default are written to the container

- `-v /dev/log:/dev/log logger "message"` to capture log

- Type journalctl | grep container to see this test log message