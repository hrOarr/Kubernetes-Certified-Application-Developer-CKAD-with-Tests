## label nodes for node affinity
```
kubectl label nodes minikube-m02 name=app-worker-node
```
## Pod definition config file for node affinity
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-test
  labels:
    env: test-env
spec:
  containers:
  - name: nginx
    image: nginx:latest
    imagePullPolicy: IfNotPresent
    resources:
      requests:
        memory: "128Mi"
        cpu: "250m"
      limits:
        memory: "512Mi"
        cpu: "500m"
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: name
            operator: In
            values:
            - app-worker-node
```

## Pod affinity config
```
affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app-name
            operator: In
            values:
            - web-app
        topologyKey: topology.kubernetes.io/zone
```
## Pod anti-affinity config
```
affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app-name
            operator: In
            values:
            - database
        topologyKey: topology.kubernetes.io/zone
```

