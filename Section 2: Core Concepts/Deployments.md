```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    app: nginx-app
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.20.2
        ports:
        - containerPort: 80
```

```
kubectl get deployments (see all deployments)

kubectl set image deployment.v1.apps/nginx nginx-app=nginx:1.23.4 (update the image)
kubectl rollout status deployment/nginx (status of rollout)
kubectl set image deployment/nginx nginx-app=nginx:1.234 (rollback)
kubectl rollout undo deployment/nginx

kubectl describe deployment nginx
kubectl scale deployment/nginx --replicas=12
kubectl autoscale deployment/nginx --min=8 --max=16 --cpu-percent=80
```
