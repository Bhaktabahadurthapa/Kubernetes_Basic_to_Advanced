### 1. Cluster Management Commands

**Cluster Information**

```
# View cluster information
kubectl cluster-info

# View version information
kubectl version

# Check cluster health
kubectl get componentstatuses

# Get API resources
kubectl api-resources

# View cluster events
kubectl get events --all-namespaces
```
**Node Management**

```
# List all nodes
kubectl get nodes
kubectl get nodes -o wide  # Detailed view

# Describe specific node
kubectl describe node <node-name>

# Label operations
kubectl label nodes <node-name> <key>=<value>
kubectl label nodes <node-name> <key>-  # Remove label

# Maintenance operations
kubectl drain <node-name>  # Drain node for maintenance
kubectl cordon <node-name>  # Mark node as unschedulable
kubectl uncordon <node-name>  # Mark node as schedulable

# Node metrics
kubectl top node <node-name>
```
### 2. Namespace Operations

**Basic Namespace Commands**
```
# List namespaces
kubectl get namespaces
kubectl get ns  # Short form

# Create namespace
kubectl create namespace <name>
kubectl create ns <name>  # Short form

# Delete namespace
kubectl delete namespace <name>
kubectl delete ns <name>  # Short form

# Describe namespace
kubectl describe namespace <name>

# Set default namespace for current context
kubectl config set-context --current --namespace=<name>
```

**3. Pod Operations**

**Basic Pod Commands**

```
# List pods
kubectl get pods
kubectl get pods -o wide  # Detailed view
kubectl get pods --all-namespaces  # Across all namespaces
kubectl get pods -l key=value  # Filter by label

# Create pod
kubectl run <pod-name> --image=<image-name>
kubectl run <pod-name> --image=<image-name> --port=<port>

# Delete pod
kubectl delete pod <pod-name>
kubectl delete pod <pod-name> --force  # Force delete
kubectl delete pods --all  # Delete all pods in current namespace

# Pod details
kubectl describe pod <pod-name>

# Pod logs
kubectl logs <pod-name>
kubectl logs <pod-name> -f  # Follow logs
kubectl logs <pod-name> --previous  # Previous container logs
kubectl logs <pod-name> -c <container-name>  # Specific container logs

# Execute commands in pod
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec <pod-name> -- <command>

# Copy files to/from pod
kubectl cp <pod-name>:/path/to/file /local/path
kubectl cp /local/path <pod-name>:/path/to/file

```
## 4. Deployment Operations

**Basic Deployment Commands**
```
# List deployments
kubectl get deployments
kubectl get deploy  # Short form

# Create deployment
kubectl create deployment <name> --image=<image>
kubectl create -f deployment.yaml

# Update deployment
kubectl apply -f deployment.yaml
kubectl set image deployment/<name> <container>=<image>

# Scale deployment
kubectl scale deployment <name> --replicas=<number>

# Delete deployment
kubectl delete deployment <name>

# Deployment status
kubectl rollout status deployment/<name>

# Deployment history
kubectl rollout history deployment/<name>

# Rollback deployment
kubectl rollout undo deployment/<name>
kubectl rollout undo deployment/<name> --to-revision=<number>

# Pause/Resume deployment
kubectl rollout pause deployment/<name>
kubectl rollout resume deployment/<name>
```

## 5. Service Operations

```
# List services
kubectl get services
kubectl get svc  # Short form

# Create service
kubectl expose deployment <name> --port=<port> --type=<type>
kubectl create -f service.yaml

# Delete service
kubectl delete service <name>

# Describe service
kubectl describe service <name>

# Update service
kubectl patch svc <name> -p '{"spec":{"type":"NodePort"}}'
```
## 6. Configuration Management
**ConfigMaps**
```
# Create ConfigMap
kubectl create configmap <name> --from-file=<path>
kubectl create configmap <name> --from-literal=key=value

# List ConfigMaps
kubectl get configmaps
kubectl get cm  # Short form

# Delete ConfigMap
kubectl delete configmap <name>

# Edit ConfigMap
kubectl edit configmap <name>
```
**Secrets**
```
# Create Secret
kubectl create secret generic <name> --from-literal=key=value
kubectl create secret tls <name> --cert=path/to/cert --key=path/to/key
kubectl create secret docker-registry <name> --docker-username=user --docker-password=pass

# List Secrets
kubectl get secrets

# Delete Secret
kubectl delete secret <name>
```
## 7. Storage Operations

**Persistent Volumes (PV)**

  ```
# List PVs
kubectl get pv

# Create PV
kubectl create -f pv.yaml

# Delete PV
kubectl delete pv <name>

# Describe PV
kubectl describe pv <name>
```
**Persistent Volume Claims (PVC)**
```
# List PVCs
kubectl get pvc

# Create PVC
kubectl create -f pvc.yaml

# Delete PVC
kubectl delete pvc <name>

# Describe PVC
kubectl describe pvc <name>
```
### 8. RBAC Operations

**Role and RoleBinding**
```
# Create Role
kubectl create role <name> --verb=get,list,watch --resource=pods

# Create RoleBinding
kubectl create rolebinding <name> --role=<role-name> --user=<user>

# List Roles/RoleBindings
kubectl get roles
kubectl get rolebindings

# Delete Role/RoleBinding
kubectl delete role <name>
kubectl delete rolebinding <name>
```
**ClusterRole and ClusterRoleBinding**
```
# Create ClusterRole
kubectl create clusterrole <name> --verb=get,list,watch --resource=pods

# Create ClusterRoleBinding
kubectl create clusterrolebinding <name> --clusterrole=<role-name> --user=<user>

# List ClusterRoles/ClusterRoleBindings
kubectl get clusterroles
kubectl get clusterrolebindings

# Delete ClusterRole/ClusterRoleBinding
kubectl delete clusterrole <name>
kubectl delete clusterrolebinding <name>
```
## 9. Network Operations

**Ingress**

```
# List Ingress
kubectl get ingress
kubectl get ing  # Short form

# Create Ingress
kubectl create -f ingress.yaml

# Delete Ingress
kubectl delete ingress <name>

# Describe Ingress
kubectl describe ingress <name>
```
**Network Policies**
```
# List Network Policies
kubectl get networkpolicies
kubectl get netpol  # Short form

# Create Network Policy
kubectl create -f networkpolicy.yaml

# Delete Network Policy
kubectl delete networkpolicy <name>
```
## 10. Debugging and Troubleshooting
**Debugging Commands**
```
# Get cluster events
kubectl get events

# Node troubleshooting
kubectl describe node <node-name>
kubectl top node

# Pod troubleshooting
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/bash

# Service troubleshooting
kubectl describe service <service-name>
kubectl get endpoints <service-name>

# Port forwarding
kubectl port-forward pod/<pod-name> <local-port>:<pod-port>
kubectl port-forward service/<service-name> <local-port>:<service-port>
```
## 11. Context and Configuration
**Context Management**
```
# List contexts
kubectl config get-contexts

# Switch context
kubectl config use-context <context-name>

# Set cluster
kubectl config set-cluster <cluster-name> --server=<server-url>

# Set credentials
kubectl config set-credentials <user-name> --token=<token>

# View config
kubectl config view
kubectl config view --minify  # Current context only
```
## 12. Resource Quotas and Limits
**Resource Management**
```
# List Resource Quotas
kubectl get resourcequotas

# Create Resource Quota
kubectl create quota <name> --hard=cpu=1,memory=1G,pods=2

# List Limit Ranges
kubectl get limitranges

# Create Limit Range
kubectl create -f limitrange.yaml
```

## Common Flags

**-n, --namespace: Specify namespace
-o, --output: Output format (json|yaml|wide|name)
-l, --selector: Label selector
-f, --filename: Filename, directory, or URL
--force: Force operation
--grace-period: Grace period (in seconds)
--all: Select all resources
--field-selector: Field selector
--show-labels: Show labels in output**
















