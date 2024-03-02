```
kubectl get ns
kubectl create namespace test
kubectl config set-context --current --namespace=<namespace-name>
kubectl run nginx --image=nginx --namespace=test
kubectl config current-context
```
