# Troubleshooting

## Procedure

- Verify syntax before adding anything

- Use standard Linux tools for troubleshooting
    - Consider starting busybox if tools are absent

- User `kubectl describe` to see what happens

- Use `kubectl logs` to see what a container in a Pod is doing

- Consider limitations: logging activity across all nodes is not part of k8s and provided by external projects like Fluentd or Prometheus

## Pods States

- In its lifetime, a Pods will go through different states:

    - `Pending`: the Pod has been validated by the API server and an entry has been created in the `ectd`, but images still need to be fetched

    - `Running`: Pod currently is successfully running

    - `Failed`: Pod has completed its work

    - `Unknown`: Pod status could not be obtained

- Current Pod status can be observed using `kubectl get pods`

## Probe

- Probes are part of the container spec and can be used to test access to Pods

- A `readinessProbe` used to make sure a Pod is not published as available until the `readinessProbe` has been able to access it

- The `livenessProbe` is used to continue checking the availability of a Pod

- A Probe is a simple test taht verifies that the app is reacting

- Probe types are defined in `pod.container.spec`:

    - `exec`: a command is executed an returns a zero exit value

    - `httpGet`: an HTTP request returns a response code between 200 and 399

    - `tcpSocket`: connectitivy to a TCP socket is successful

## Monitoring

- The goal of monitoring is to collect metrics about the infrastructure

- k8s monitoring happens through external CNCF projects

- `Heapster` is a part of k8s and can be used for monitoring multiple pods

- `Prometheus` is available as k8s plugin and provides cross cluster usage metrics

- `Fluentd`: can aggregrate logs

### Commands

- `kubectl get pods -o wide`
