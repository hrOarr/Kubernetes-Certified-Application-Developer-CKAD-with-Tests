## Resource request snippet
```
apiVersion: v1
kind: Pod
metadata:
  name: requests-demo
spec:
  containers:
    - name: nginx
      image: nginx:latest
      resources:
        requests:
          cpu: "100m"
          memory: "150Mi"
```

## Resource limit snippet
```
apiVersion: v1
kind: Pod
metadata:
  name: limits-demo
spec:
  containers:
    - name: nginx
      image: nginx:latest
      resources:
        limits:
          cpu: 100m
          memory: 150Mi
```

## Best Practices for Setting Kubernetes Requests and Limits
 - Don't use CPU limits
 - Always Set Equal Memory Requests and Limits
 - Regularly Review and Rightsize Your Requests and Limits
