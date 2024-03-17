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

## Namespace ResourceQuota
With ResourceQuotas, you can set a memory or CPU limit to the entire namespace, ensuring that entities in it can’t consume more from that amount.
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: mem-cpu-demo
spec:
  hard:
    requests.cpu: 2
    requests.memory: 1Gi
    limits.cpu: 3
    limits.memory: 2Gi
```

## Namespace LimitRange
LimitRanges are a Kubernetes policy that restricts the resource settings for each entity in a namespace.
```
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-resource-constraint
spec:
  limits:
  - default:
      cpu: 500m
    defaultRequest:
      cpu: 500m
    min:
      cpu: 100m
    max:
      cpu: "1"
    type: Container
```
