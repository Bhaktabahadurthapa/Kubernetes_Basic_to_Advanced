# Persistent Volume (PV) and Persistent Volume Claim (PVC)

Create a Persistent Volume (PV)
First, create a YAML file named pv.yaml
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: task-pv
  labels:
    type: local
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  hostPath:
    path: "/mnt/data"
```
Apply the PV: and Check if PV is created:
```
kubectl apply -f pv.yaml
kubectl get pv
kubectl describe pv task-pv
```
Create a Persistent Volume Claim (PVC)
Create a file named pvc.yaml:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pvc
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

Apply the PVC and Verify PVC
```
kubectl apply -f pvc.yaml
kubectl get pvc
kubectl describe pvc task-pvc
```

Create a Pod using the PVC
Create a file named pod.yaml:
```
apiVersion: v1
kind: Pod
metadata:
  name: task-pod
spec:
  containers:
  - name: task-container
    image: nginx
    volumeMounts:
    - mountPath: "/usr/share/nginx/html"
      name: task-volume
  volumes:
  - name: task-volume
    persistentVolumeClaim:
      claimName: task-pvc

```
Apply the Pod and Verify Pod:
```
kubectl apply -f pod.yaml
kubectl get pods
kubectl describe pod task-pod
```
Test the Storage Connect to the pod:
```
kubectl exec -it task-pod -- /bin/bash
```
Create a test file:
```
echo "Hello from Kubernetes storage" > /usr/share/nginx/html/test.txt
```
Exit the pod:

after that, Verify Data Persistence
Delete the pod:
```
kubectl delete pod task-pod
```
Recreate the pod:
```
kubectl apply -f pod.yaml
```
Check if data persists:
```
kubectl exec -it task-pod -- cat /usr/share/nginx/html/test.txt
```














