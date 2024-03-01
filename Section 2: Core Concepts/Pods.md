kubectl get pods (see list of pods in default namespace)

kubectl get pods -n <namespace-name> (see list of pods in specific namespace)

kubectl get pods --all-namespaces (see list of pods in all namespaces)

kubectl describe pods <pod-name>


kubectl run nginx --image nginx:latest (create a pod)

kubectl create deployment nginx --image nginx:latest --replicas 3 (create a deployment)

kubectl scale deployment nginx --replicas 5 (scale a deployment)


kubectl expose deployment/nginx --port 80 --type NodePort (expose a service)

kubectl get nodes -o wide (see details of pods)

### Declarative approach to create a pod

```

apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
	- name: nginx
	  image: nginx:latest
   
```
kubectl apply -f nginx.yaml (create pod using file)
