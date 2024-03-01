![alt text](https://github.com/hrOarr/Kubernetes-Certified-Application-Developer-CKAD-with-Tests/blob/f541a8f8c45a80b6cabadf026bb5e60b3a5ca3ae/Section%202%3A%20Core%20Concepts/k8s-architecture.drawio-1.png)

# Architecture Terms
 - Nodes (Minions)
 - Cluster (set of nodes)
 - Control Plane (Master)
 - Worker Nodes


# High level components
## Control Plane
 - kube-apiserver
 - etcd
 - kube-scheduler
 - kube-controller-manager
 - cloud-controller-manager

## Worker Node
 - kubelet
 - kube-proxy
 - Container runtime

# Control Plane Components
 - **Kube API server**
   ### Use cases
   - API Management
   - Authentication
   - Only components that communicate with **etcd**
     
   ![alt text](https://github.com/hrOarr/Kubernetes-Certified-Application-Developer-CKAD-with-Tests/blob/f2ed3c69c7d37a223e3f1c152e0826fcdc2e929f/Section%202%3A%20Core%20Concepts/kube-api-server.drawio-2.png)

- **etcd**
  
   It acts as both a backend service discovery and a database. You can call it the brain of the Kubernetes cluster.
   ### Use cases
    - Strongly consistent
    - Distributed
    - Key-value store
    - Stores all configurations, states, and metadata of Kubernetes objects (pods, secrets, daemonsets, deployments, configmaps, statefulsets, etc).It acts as both a backend service discovery and a database. You can call it the brain of the Kubernetes cluster.
    - Allows a client to subscribe to events using Watch() API . Kubernetes api-server uses the etcd’s watch functionality to track the change in the state of an object.
    - Exposes key-value API using gRPC. Also, the gRPC gateway is a RESTful proxy that translates all the HTTP API calls into gRPC messages. This makes it an ideal database for Kubernetes.
    - Stores all objects under the /registry directory key in key-value format. For example, information on a pod named Nginx in the default namespace can be found under /registry/pods/default/nginx
  
- **Kube Scheduler**
  
   The kube-scheduler is responsible for scheduling Kubernetes pods on worker nodes.

   When you deploy a pod, you specify the pod requirements such as CPU, memory, affinity, taints or tolerations, priority, persistent volumes (PV),  etc. The scheduler’s primary task is to identify the create request and choose the best node for a pod that satisfies the requirements.
   - It is a controller that listens to pod creation events in the API server.
   - The scheduler has two phases. Scheduling cycle and the Binding cycle. Together it is called the scheduling context. The scheduling cycle selects a worker node and the binding cycle applies that change to the cluster.
   - Custom scheduler can be added

- **Kube Controller Manager**
  
   In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state.

   Following is the list of important built-in Kubernetes controllers.
   - Deployment controller
   - Replicaset controller
   - DaemonSet controller
   - Job Controller (Kubernetes Jobs)
   - CronJob Controller
   - endpoints controller-
   - namespace controller
   - service accounts controller.
   - Node controller
- **Cloud Controller Manager (CCM)**
  
   When kubernetes is deployed in cloud environments, the cloud controller manager acts as a bridge between Cloud Platform APIs and the Kubernetes cluster.

   This way the core kubernetes core components can work independently and allow the cloud providers to integrate with kubernetes using plugins. (For example, an interface between kubernetes cluster and AWS cloud API)
   Cloud controller integration allows Kubernetes cluster to provision cloud resources like instances (for nodes), Load Balancers (for services), and Storage Volumes (for persistent volumes).


# Worker Node Components
 - **Kubelet**
   
   Kubelet is an agent component that runs on every node in the cluster. t does not run as a container instead runs as a daemon, managed by systemd.
   It is responsible for registering worker nodes with the API server and working with the podSpec (Pod specification – YAML or JSON) primarily from the API server. podSpec defines the containers that should run inside the pod, their resources (e.g. CPU and memory limits), and other settings such as environment variables, volumes, and labels.

   To put it simply, kubelet is responsible for the following.
   - Creating, modifying, and deleting containers for the pod.
   - Responsible for handling liveliness, readiness, and startup probes.
   - Responsible for Mounting volumes by reading pod configuration and creating respective directories on the host for the volume mount.
   - Collecting and reporting Node and pod status via calls to the API server with implementations like cAdvisor and CRI.
   - Kubelet uses the CRI (container runtime interface) gRPC interface to talk to the container runtime.
   - It also exposes an HTTP endpoint to stream logs and provides exec sessions for clients.
   - Uses the CSI (container storage interface) gRPC to configure block volumes.
   - It uses the CNI plugin configured in the cluster to allocate the pod IP address and set up any necessary network routes and firewall rules for the pod.

 - **Kube Proxy**

   Kube-proxy is a daemon that runs on every node as a daemonset. It is a proxy component that implements the Kubernetes Services concept for pods. (single DNS for a set of pods with load balancing). It primarily proxies UDP, TCP, and SCTP and does not understand HTTP.
   
   When you expose pods using a Service (ClusterIP), Kube-proxy creates network rules to send traffic to the backend pods (endpoints) grouped under the Service object. Meaning, all the load balancing, and service discovery are handled by the Kube proxy.

 - **Container Runtime**

   Container runtime runs on all the nodes in the Kubernetes cluster. It is responsible for pulling images from container registries, running containers, allocating and isolating resources for containers, and managing the entire lifecycle of a container on a host.

   To understand this better, let’s take a look at two key concepts:
    - Container Runtime Interface (CRI): It is a set of APIs that allows Kubernetes to interact with different container runtimes. It allows different container runtimes to be used interchangeably with Kubernetes. The CRI defines the API for creating, starting, stopping, and deleting containers, as well as for managing images and container networks.
    - Open Container Initiative (OCI): It is a set of standards for container formats and runtimes


## Useful resources
 - https://devopscube.com/kubernetes-architecture-explained/
