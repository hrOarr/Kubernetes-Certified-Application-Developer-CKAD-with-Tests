## Concept
Taints and tolerations are a mechanism that allows you to ensure that pods are not placed on inappropriate nodes. Taints are added to nodes, 
while tolerations are defined in the pod specification. When you taint a node, it will repel all the pods except those that have a toleration for that taint. 
A node can have one or many taints associated with it.

## Taint a node
```
kubectl taint nodes <node name> <taint key>=<taint value>:<taint effect>
```

## Each taint consists of three parts:

**Key**: The key represents the name of the taint and is used to uniquely identify it.

**Value**: An optional value associated with the taint key.

**Effect**: The effect determines how the taint affects pod scheduling.

## There are three possible values for the effect:

**NoSchedule**: Prevents new pods from being scheduled on the tainted node.

**PreferNoSchedule**: Similar to NoSchedule, but the scheduler tries to avoid placing new pods on the tainted node unless necessary.

**NoExecute**: Evicts existing pods that do not tolerate the taint.

## Add tolerations in a Pod
```
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
  - name: my-app
    image: my-app-image
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "test"
    effect: "NoSchedule"
```
