# Persistent Volume (PV)

## Sample Storage
First create `pv.yml` file:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv0001
spec:
  accessModes:
  - ReadWriteOnce
capacity:
  storage: 5Gi
hostPath:
  path: /tmp/pvs_data/pv0001
```

Next create `pvc.yml` file:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myClaim
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

Next create the pv and pvc:
```sh
$ kubectl create -f pv.yml
$ kubectl create -f pvc.yml
```

Then attach it to pods:
```yaml
...
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    ports:
    - containerPort: 80
    volumeMounts:
    - mountPath: "/usr/share/nginx/html"
      name: mypd
  volumes:
  - name: mypd
    persistentVolumeClaim:
      claimName: myclaim
```

## Commands
```sh
# get all pvs and claims
$ kubectl get pv
# get all pvcs
$ kubectl get pvc
```