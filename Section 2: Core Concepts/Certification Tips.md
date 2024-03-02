```
## Pod
kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx-pod.yaml

## Deployment
kubectl create deployment --image=nginx nginx
kubectl create deployment nginx --image=nginx--dry-run=client -o yaml > nginx-deployment.yaml

## Service
**Create a Service named redis-service of type **ClusterIP** to expose pod redis on port 6379:

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
(This will automatically use the pod's labels as selectors)

Or

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml
(This will not use the pods' labels as selectors; instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work well if your pod has a different label set. So generate the file and modify the selectors before creating the service)


**Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:

kubectl expose pod nginx --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
(This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.)

Or

kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
(This will not use the pods' labels as selectors)

```
