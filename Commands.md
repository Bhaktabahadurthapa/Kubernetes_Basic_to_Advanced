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





























