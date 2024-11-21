**Kubernetes Basics**

**👉 What is Kubernetes?**
Overview of Kubernetes and why it's used in production environments
Understanding Kubernetes clusters, nodes, and pods
How Kubernetes fits into the DevOps lifecycle

**👉 Kubernetes Architecture**
Master node, worker nodes, and control plane
Components: API server, controller manager, scheduler, kubelet, kube-proxy
Understanding Pods, ReplicaSets, Deployments, Services, Namespaces

**👉 Setting Up a Kubernetes Cluster**
Local Kubernetes with Minikube or Kind (Kubernetes IN Docker)
Setting up clusters in the cloud: EKS (AWS), GKE (Google Cloud), AKS (Azure)
Introduction to Kubernetes as a Service (KaaS)

**👉 Basic Kubernetes Operations**
kubectl basics: commands, contexts, namespaces
Deploying applications using kubectl apply, kubectl get, kubectl describe
Scaling applications, rolling updates, and monitoring pod health


**Intermediate Kubernetes Concepts**

**👉 Pods and Controllers**
Pod lifecycle: init containers, multi-container pods
ReplicaSets and Deployments for scaling applications
StatefulSets vs Deployments for stateful applications

**👉 Services and Networking**
ClusterIP, NodePort, LoadBalancer services
Ingress controllers and setting up Ingress resources for HTTP(S) routing
DNS and Service Discovery in Kubernetes
Networking policies (e.g., Calico or Cilium)

**👉  Storage in Kubernetes**
Persistent Volumes (PV) and Persistent Volume Claims (PVC)
Storage Classes, dynamic provisioning, and cloud storage integration (e.g., EBS, GCE persistent disks)
Stateful applications and database persistence

**👉  Helm Package Manager**
Understanding Helm charts and their usage for deploying applications
Installing, upgrading, and managing Helm releases
Creating custom Helm charts for managing deployments

