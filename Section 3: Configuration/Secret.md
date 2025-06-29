```
kubectl create secret generic apikey --from-literal=API_KEY=123–456
kubectl describe secret apikey
```

```
## Secret YAML file
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=  # base64 encoded 'admin'
  password: MWYyZDFlMmU2N2Rm  # base64 encoded '1f2d1e2e67df'
```

```
## Reference to Pod - 1
apiVersion: v1
kind: Pod
metadata:
  name: secret-env-pod
spec:
  containers:
  - name: mycontainer
    image: redis
    env:
      - name: SECRET_USERNAME
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: username
      - name: SECRET_PASSWORD
        valueFrom:
          secretKeyRef:
            name: mysecret
            key: password
  restartPolicy: Never

## Reference to Pod - 2
apiVersion: v1
kind: Pod
metadata:
  name: secret-env-pod
spec:
  containers:
  - name: mycontainer
    image: redis
    envFrom:
     - secretRef:
         name: mysecret
  restartPolicy: Never
```

```
## Container startup commands with secrets
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: myapp
    command: [ "/app/start", "--token" ]
    args:
    - valueFrom:
        secretKeyRef:
          name: mysecret
          key: token
  restartPolicy: Never
```
