```
## Environment variables in Pod
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: my-app-image
      env:
        - name: DATABASE_URL
          value: "mysql://user:password@db-host:3306/database"
        - name: API_KEY
          value: "your-api-key"

## imperative approach
kubectl run nginx --image=nginx -e DB_URL=<url>

```

```
kubectl create configmap <configmap-name> --from-literal=<key>=<value>
kubectl create configmap <configmap-name> --from-file=<file-path>

```
```
## Declarative
**ConfigMap:
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  DATABASE_URL: "mysql://user:password@db-host:3306/database"
  API_KEY: "your-api-key"

**Reference to Pod
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: my-app-image
      envFrom:
        - configMapRef:
            name: my-config
```
