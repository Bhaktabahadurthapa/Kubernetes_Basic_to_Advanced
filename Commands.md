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


