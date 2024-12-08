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
**To apply this role:**
```
kubectl apply -f role.yaml
```
**To check the created role:**
```
kubectl get role
```

**Role Binding**

The rolebinding.yaml file defines a role binding named read-pods that binds the pod-reader role to the user jack in the default namespace.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: jack
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
**To apply this role binding:**
```
kubectl apply -f rolebinding.yaml
```
**To check the created role binding:**
```
kubectl get rolebinding
```
**To check the permissions of the jack user:**
```
kubectl auth can-i get pod --as jack
```






























