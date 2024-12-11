# Configmap

### by using volume 
```
 apiVersion: v1
kind: Pod
metadata:
  name: myvolconfig
spec:
  containers:
name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; via mount file volume; sleep 5 ; done"]
    volumeMounts:
name: testconfigmap
        mountPath: "/tmp/config"   # the config files will be mounted as ReadOnly by default here
  volumes:
name: testconfigmap
    configMap:
       name: mymap   # this should match the config map name created in the first step
       items:
key: sample.conf
         path: sample.conf
```

**By Using Env variable**
```
apiVersion: v1
kind: Pod
metadata:
  name: myenvconfig
spec:
  containers:
name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; by env ; sleep 5 ; done"]
    env:
name: MYENV         # env name in which value of the key is stored
      valueFrom:
        configMapKeyRef:
          name: mymap      # name of the config created
          key: sample.conf

```
# create a Secrets Map
```
apiVersion: v1
kind: Pod
metadata:
  name: myvolsecret
spec:
  containers:
name: c1
    image: centos
    command: ["/bin/bash", "-c", "while true; create a secret; sleep 5 ; done"]
    volumeMounts:
name: testsecret
        mountPath: "/tmp/mysecrets"   # the secret files will be mounted as ReadOnly by default here
  volumes:
name: testsecret
    secret:
       secretName: mysecret
```

