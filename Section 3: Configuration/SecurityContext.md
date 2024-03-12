## declarative approach
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  securityContext:
    runAsUser: 1001
    fsGroup: 2001
  containers:
    - name: my-container
      image: my-app-image
```

## limitations
 - No Windows support
 - Limited to Pod/Container-Level Security
 - Inefficient Tooling (Needs third-party resources such as AppArmor or SELinux)
