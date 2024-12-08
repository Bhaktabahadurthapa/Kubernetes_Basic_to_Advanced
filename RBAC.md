This guide provides instructions for creating roles, cluster roles, role bindings, and cluster role bindings in a Kubernetes cluster. RBAC (Role-Based Access Control) allows you to control access to resources within the cluster based on user roles and permissions.

**Role**
The role.yaml file contains the configuration for creating a role named pod-reader. The role allows the user to perform actions like get, watch, and list on pods resources.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```
