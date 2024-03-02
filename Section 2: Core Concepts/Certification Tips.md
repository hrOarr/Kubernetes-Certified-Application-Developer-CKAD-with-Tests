```
## Pod
kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx-pod.yaml

## Deployment
kubectl create deployment --image=nginx nginx
kubectl create deployment nginx --image=nginx--dry-run=client -o yaml > nginx-deployment.yaml

## Service
Create a Service named redis-service of type **ClusterIP** to expose pod redis on port 6379

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

(This will automatically use the pod's labels as selectors)

Or

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml (This will not use the pods' labels as selectors; instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work well if your pod has a different label set. So generate the file and modify the selectors before creating the service)

```
