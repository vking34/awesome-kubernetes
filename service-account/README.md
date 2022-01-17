# Service Account

- All actions in k8s cluster need to be authenticaed and authorized

- `Service Account (sa)` is used for basic authen from within the k8s cluster

- `ServiceAccount (sa)` exists as a separate API resource

- Roles and role bindings are used for authorizatoin

- Every Pod uses the Default SA to contact the API server

- This default SA allows a resource to get info from API server, but not much else

- Each SA uses a secret to automount API credentials

## Secrets

- SA comes with a secret

- This secret contains API credentials

- By specifying the SA to be used by a pod, the SA secret is auto-mounted to provide API access credentials

## Permissions

- a cluster admin can configure RBAC authorization to specify what exactly can be accessed by a SA

- Custom SA can be created and configured with additional permissions

- For additional permissions, namespace or cluster scope roles and rolebindings are used


## Managing

- Every namespace has a default SA called `default`

- Additional service accounts can be created to provide additional access to resources

- After creating the additional service account, authorization needs to be set up

- SA(s) are easily created using declarative or imperative way

- While creating a SA, a secret is automatically creatd to have the SA connect to the API

- This secret is mounted in Pods using the SA

- Authorization plugins can be used to set permissions on SA

- `kubectl create serviceaccount mysa`
