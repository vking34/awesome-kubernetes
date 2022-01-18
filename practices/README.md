# Practices

### Create a NameSpace `ckad-ns1` in your cluster. In this NameSpace, run the following Pods:
- A pod with the name `pod-a`, running the httpd sever image

- A pod with the name `pod-b`, running the nginx server image as well as the alpine image

<details><summary>show</summary>
<p>

```bash
k create ns ckad-ns1

k run pod-a --image=httpd --restart Never -n ckad-ns1

```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-b
  namespace: ckad-ns1
spec:
  containers:
  - name: nginx
    image: nginx
  - name: alpine
    image: alpine
    command: ['sleep', '3600']

```

</p>
</details>

#
### The pod my-server is running 3 containers: file-server, log-server, and db-server. When starting it, the log-server fails. Which command should you use to analyze why it is going wrong?

<details><summary>show</summary>
<p>

```bash
kubectl -n ns1 logs my-server -c log-server 
```

</p>
</details>


#
### Create a pod that runs the nginx webserver
- The webserver should be offering its services on port 80 and run in the `ckad-ns3` namespace

- This pod should use a readiness probe that gets 60 seconds to complete

- The probe should check the availability of the webserver document root (path `/var/www/html`) before start and during operation as well


<details><summary>show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  namespace: ckad-ns3
spec:
  containers:
  - name: webserver
    image: nginx
    ports:
    - containerPort: 80
    readinessProbe:
      exec:
        command: ['ls', '/']
      initialDelaySeconds: 60
      periodSeconds: 60
```

</p>
</details>

#
### Write a manifest file with the name `nginx-exam.yaml` that meets the following requirements:
- It starts 5 replicas that run the `nginx:1.8` image

- Each pod has the label `app=webshop`

- Create the Deployment such that while updating the existing pods are terminated before new pods are created to replace them

- The Deployment itself should use the label `service=nginx`

<details><summary>show</summary>
<p>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    service: nginx
spec:
  replicas: 5
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: webshop
  template:
    metadata:
      labels:
        app: webshop
    spec:
      containers:
      - name: nginx
        image: nginx:1.8
        ports:
        - containerPort: 80

```

</p>
</details>

#
### In the `ckad-ns6` NameSpace, create a Deployment that runs the `nginx:1.9` image and give it the name `nginx-deployment`:

- Ensure it run 3 replicas

- After verifying that the Deployment runs successfully, expose it such that users that are external to the cluster can reach it, using the k8s Service


<details><summary>show</summary>
<p>

```bash
k create ns ckad-ns6

k -n ckad-ns6 create deployment nginx-deployment --image nginx:1.9 --replicas 3

k -n ckad-ns6 expose deployment nginx-deployment --port 80 --type NodePort
```

</p>
</details>


#
### Create a YAML file with the name `my-nw-policy` that runs 2 pods and a NetworkPolicy

- The pods may be dummies and dont really have to provide specific functionality as long as they will running for at least 3600 seconds

- One pod similates running a database, the other pod simulates running a webserver

- Use a NetworkPolicy to restrict traffic between pods in the following way:
    - Incoming and outgoing traffic to the webserver is allowed without any restrictions

    - Only the webserver is allowed to access the database

    - No outgoing traffic is allowed from the database pod


<details><summary>show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web
  labels:
    app: web
spec:
  containers:
  - name: web
    image: alpine
    command: ['sleep', '3600']

---
apiVersion: v1
kind: Pod
metadata:
  name: db
  labels:
    app: db
spec:
  containers:
  - name: db
    image: alpine
    command: ['sleep', '3600']

---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-np
spec:
  policyTypes:
  - Ingress
  - Egress
  podSelector:
    matchLabels:
      app: db
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: web

```

</p>
</details>


#
### All object in this assignment should be created in the `ckad-1312` namespace

- Create a PV with the name `1312-pv`. It should provide 2 GB of storage and read/write access tot multiple clients simultaneously. Use any storage type u like

- Next, create a PVC that request 1 GB from any PV that allows multiple clients simultaneous read/write access. The name of the object should be `1312-pvc`

- Finally, create a Pod with the name `1312-pod` that uses this persistent volume. It should run an `nginx` image, and mount the volume on the directory `/webdata`


<details><summary>show</summary>
<p>

```yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: 1312-pv
  labels:
    type: local
  namespace: ckad-1312
spec:
  storageClassName: manual
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/mnt/data"

---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: 1312-pvc
  namespace: ckad-1312
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi

---
apiVersion: v1
kind: Pod
metadata:
  name: 1312-pod
  namespace: ckad-1312
spec:
  volumes:
    - name: 1312-storage
      persistentVolumeClaim:
        claimName: 1312-pvc
  containers:
    - name: 1312-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/webdata"
          name: 1312-storage


```

</p>
</details>

