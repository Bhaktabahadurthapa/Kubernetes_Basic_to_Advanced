# Persistent Volume (PV) and Persistent Volume Claim (PVC)


<img width="781" alt="image" src="https://github.com/user-attachments/assets/0b0b4a32-1b7f-4aca-a2d6-6122a97058e0" />

Figure: Basic PV and PVC Workflow in Kubernetes





<img width="368" alt="image" src="https://github.com/user-attachments/assets/b69fba43-e200-4e76-881f-c5d9fb364ad6" />

Figure Shows: PV Lifecycle States



<img width="474" alt="image" src="https://github.com/user-attachments/assets/46b6809b-10de-41fe-a977-37a0ede2ea86" />

Figure: Namespace Level Storage



```
Basic Flow:

Physical storage is abstracted as PV
PVC claims the storage
Pod uses the PVC


Lifecycle:

Available: PV is free to use
Bound: PV is claimed by a PVC
Released: PVC is deleted but PV not yet reclaimed


Namespace Level:

PVs exist at cluster level
PVCs are namespace specific
Different namespaces can use different PVs
```
      
# Create a Persistent Volume (PV)
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

# Create a Persistent Volume Claim (PVC)
Create a file named pvc.yaml:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pvc
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
```

Apply the PVC and Verify PVC
```
kubectl apply -f pvc.yaml
kubectl get pvc
kubectl describe pvc task-pvc
```
# Note that, in GKE (Google Kubernetes Engine), we can't use hostPath directly as the node's filesystem is read-only. Let's fix this by using GCP's persistent disk instead.
Create a StorageClass (storage-class.yaml):
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/gce-pd
parameters:
  type: pd-standard
  replication-type: none
```

# Create a Pod using the PVC
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














