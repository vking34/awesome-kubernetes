# Pod Palacement

## Taint & Tolerantion

- Tolerations are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints. They allow __a node to repel a set of pods__

- Note that __Taint & Tolerantion do not guarantee that pods will only prefer these pods. In other words, a pod with a toleration can ends up on a node with the matching taint__

## Node Selector

- Node selector allows pods to be eligible to run on a node, the node must have each of the indicated key-value pairs as labels.

- `nodeSelector` provides a very simple way to constrain pods to nodes with particular labels

### Affinity

- Node affinity is conceptually similar to `nodeSelector`. The affinity/anti-affinity feature, greatly expands the types of `nodeSelector` constraints.

- Affinity allows you to constrain which nodes your pod is eligible to be scheduled on, based on labels on the node.

- Note that __affinity does not guarantee that other pods are not placed on the labeled nodes__