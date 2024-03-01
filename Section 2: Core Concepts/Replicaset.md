```
# Declarative approach to create a replicat set

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```

```

kubectl get rs (see list of replicaset)
kubectl get pods -l app=my-app (filter by label)
kubectl scale replicaset my-rs --replicas=5

```
