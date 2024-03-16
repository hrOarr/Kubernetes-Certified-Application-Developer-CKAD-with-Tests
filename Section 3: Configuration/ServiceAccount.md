```
As the name suggests, the service accounts are for the services or the non-human users in Kubernetes. It can perform all the tasks that the K8s API allows like human users.
Kubernetes by default creates a service account in each namespace of a cluster and call it a default service account. These default service accounts are mounted to every pod launched.
```

## create service account
```
kubectl create serviceaccount my-service-account
```
```
In the K8s version before 1.24, every time we would create a service account, a non-expiring secret token (Mountable secrets & Tokens) was created by default.
However, from version 1.24 onwards, it was disbanded and no secret token is created by default when we create a service account.
```

```
From version 1.22 onwards, Kubernetes introduced TokenRequest API. A token generated through this API is a time-bound token that expires after a time.
It applies to both — the default service account and the custom-defined service accounts.

kubectl create token my-time-bound-token (to create a time-bound token)
```

## Configure a service account into a pod
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  serviceAccountName: my-service-account
  automountServiceAccountToken: true
```

## Using the service account in a pod
The service account that we create above, does not contain any permission. Once we have created a role and role binding, we can use the service account to perform the specified task.
```
kubectl exec -it my-pod-with-service-account bash

TOKEN=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token) (store it in a variable)

curl -H "Authorization: Bearer $TOKEN" https://kubernetes/api/v1/namespaces/default/pods/ --insecure (curl request to K8S API)
```
