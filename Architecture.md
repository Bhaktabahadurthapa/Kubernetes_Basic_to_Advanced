## High-Level Architecture
Kubernetes follows a master-worker (control plane and data plane) architecture with these main components:

***Control Plane Components (Master Node)*** 
```
API Server: The front-end interface for the Kubernetes control plane
etcd: Distributed key-value store for cluster data
Scheduler: Places containers based on resource requirements
Controller Manager: Manages various controllers for nodes, replication, etc.
```

***Worker Node Components:***
```
Kubelet: Primary node agent that ensures containers are running
Container Runtime: Software responsible for running containers (like Docker)
Kube-proxy: Network proxy implementing Kubernetes networking services
Pods: Smallest deployable units holding one or more containers
```

https://github.com/LondheShubham153/kubestarter/blob/main/kubernetes_architecture.md 
<img width="947" alt="image" src="https://github.com/user-attachments/assets/3b7461f3-aad1-4f5e-9f24-8657df61e5d5">

### Control Plane Components in Detail:
```
a) API Server

Acts as the front-end for Kubernetes control plane
Handles all API calls, whether from kubectl, controller manager, or other components
Validates and processes REST operations
Serves as the cluster gateway

b) etcd

Consistent and highly-available key-value store
Stores all cluster data, including:

Node information
Pod states
Config maps
Secrets

Critical for cluster state management

c) Scheduler

Watches for newly created pods with no assigned node
Assigns pods to nodes based on various factors:

Resource requirements
Hardware/software/policy constraints
Affinity/anti-affinity specifications
Data locality


d) Controller Manager

Runs controller processes
Node Controller: Monitors node health
Replication Controller: Maintains correct pod counts
Endpoints Controller: Populates endpoint objects
Service Account & Token Controllers: Create default accounts and API access tokens

```

### Worker Node Components in Detail:
```
a) Kubelet

Ensures containers are running in a pod
Handles container lifecycle operations
Reports node and pod status to API server
Runs container health checks

b) Container Runtime

Responsible for running containers
Common runtimes include:

containerd
CRI-O
Docker (legacy)



c) Kube-proxy

Maintains network rules on nodes
Handles pod-to-pod and external-to-pod networking
Implements service abstraction
Performs connection forwarding

```
### Networking Architecture:
```

Pod Network: Flat networking space where all pods can communicate
Service Network: Abstract way to expose applications
NodePort: Exposes service on each node's IP
LoadBalancer: Exposes service externally using cloud provider's load balancer
Ingress: HTTP/HTTPS routing to services

Security Architecture:

Role-Based Access Control (RBAC)
Network Policies
Pod Security Policies
Service Accounts
Secrets Management

Storage Architecture:

Persistent Volumes (PV)
Persistent Volume Claims (PVC)
Storage Classes
Volume Types (EmptyDir, HostPath, NFS, Cloud Volumes)
```
