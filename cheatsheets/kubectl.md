# Kubectl

### Show logs
```
k logs sleepy
```

### Run bash shell in pod
```
kubectl exect -it pod /bin/bash

kubectl exect -it sidecar-pod -c sidecar /bin/bash
```