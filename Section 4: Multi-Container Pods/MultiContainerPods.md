## Multi-Container Design Patterns
- Adapter Pattern
- Ambassador Pattern
- Sidecar Pattern

![image](https://github.com/hrOarr/Kubernetes-Certified-Application-Developer-CKAD-with-Tests/assets/38363216/822f51bf-6c8b-4f25-95ea-a4e039862281)

## Shared Network Namespace
All the containers in the pod share the same network namespace, therefore all containers can communicate with each other on the localhost. For instance, We have two containers in the same pod listening on ports 8080 and 8081 respectively. Container 1 can talk to container 2 on localhost:8080.

## Shared Storage Volumes
All the containers can have the same volume mounted so that they can communicate with each other by reading and modifying files in the storage volume.

## Shared Process Namespace
Another way for the containers to communicate is with the Shared Process Namespace. With this, the containers inside the pod can signal each other. For this to be enabled, we need to have this setting _shareProcessNamespace _ to true in the pod spec.
