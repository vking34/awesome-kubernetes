## Secret

- Secrets allow for storage of sensitive data such as passwords, tokens, keys,...

- Using Secrets makes sense, so the data doesnt have to be put in a Pod, and reduces the risk of accidental exposure

- Some Secrets are automatically created by the system, users can also use Secrets

- Secrets are used by Pods in the way that ConfigMaps are used. They can also created by the Kubelet while pulling an image

- Secrets are not encrypted, they are encoded. If you need tight security, you need something else.


## Types

- `docker-registry`: used for connecting to a Docker registry

- `TLS`: creates a TLS Secret

- `generic`: creates a Secret from a local file, directory or literal value

## Built-in Secrets

- k8s automatically creates Secrets that contain credentials for accessing the API, and automatically modifies the Pods to use this type of Secret

- Use `kubectl describe pods <podname>` and look for the mount section to see them


## Creating Secrets

- Creating Secrets is very similar to creating ConfigMaps

- Use `kubectl create secret ... --from-file=...` to create it from a file

- Use `kubectl create secret ... --from-literal=...` to create it from a string provided on the command line

- Use YAML files:

    - When creating Secrets from YAML files, they must first be encoded using `base64`
    ```
    echo <string> | base64
    ```

    - Note that encoded is not the same as encrypted, users can easily decode using `echo <string> | base64 -d`
