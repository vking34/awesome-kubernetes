# Kubectl

### Show logs
```
k logs sleepy

k logs -f pod_name
```

### Run bash shell in pod
```
kubectl exec -it pod-name -- /bin/bash

kubectl exec -it sidecar-pod -c sidecar /bin/bash
```

