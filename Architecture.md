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
