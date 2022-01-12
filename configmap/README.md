# ConfigMap

- ConfigMaps and Secrets are special types of volumes

- ConfigMaps can be used to separtate dynamic data, typically provided as `key:value` pairs from static data in a Pod

- They can be used in three different ways:
    - Make variables available within a Pod

    - Provide command line arguments

    - Mount them on the localtion where the app expects to find a config file

    - When mounting a ConfigMap as a volume, in the mount point files will be created with the name of the Key and inside it you will find Value

- Secrets are encoded ConfigMaps which can be used to store sensitive data

- ConfigMaps can be created from different sources
    
    - `Directories`: uses multiple files in a directory

    - `Files`: puts the contents of a file in the ConfigMap

    - `Literal Vaules`: useful to provide variables and command arguments that are to used by a Pod

- Since K8S 1.14 the kustomization.yaml generator can be used
    - this uses the configMapGenerator API object to generate the ConfigMap based on input data in the kustomization.yaml

- Start by defining the ConfigMap and create it:

    - Consider the different sources that can be used for ConfigMaps

    - `kubectl create cm variables --from-env-file=variables`

    - `kubectl create cm special --from-literal=VAR3=red --from-literal=VAR4=blue`

    - Verify creation, using `kubectl describe cm <cmname>`

- Note that it doesnt really matter from which the ConfigMap is created, usage from within the Pod will be the same:
```
envFrom:
    - configMapRef:
        name: ConfigMapName
```

- ConfigMaps can alse be used to provide complete config files

- In this, the Pod is using the ConfigMap as a mounted volume which will just contain the config file

- And the ConfigMap itself contains the config file

