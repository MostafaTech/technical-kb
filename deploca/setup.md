# Setup the server

## 0 - Settings and definitions
* Server domain name is: `k8srv.local`\
* Docker Registry Port: `5000`
```sh
# append the domain name to hosts file
$ echo "127.0.0.1  k8srv.local" > /etc/hosts
```

## 1 - Setup master docker
* [Install Docker](../docker/index.md#Installation)
* [Create and run private registry](../docker/private-registry.md)


## 2 - Setup Kubernetes
* [Install Kubernetes](../kubernetes/index.md#Installation)
* Set kubernetes to pull images from the private registry:\
  *As kubernetes has multiple implementions and any one of them has different configurations, we have to set the docker registry mirror different ways.*
  * [K3S way](../kubernetes/impl-k3s.md#Change-registrymirrors-to-private)
* Restart the kubernetes service


## 3 - Setup Reverse Proxy


## 4 - Deploy an app
Create a sample `vuecon-iran-deployment.yml` file with following contents:
```yaml
# deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vuecon-iran-deployment
spec:
  selector:
    matchLabels:
      app: vuecon-iran
  replicas: 2
  template:
    metadata:
      labels:
        app: vuecon-iran
    spec:
      containers:
      - name: vuecon-iran
        image: k8srv.local:5000/vuecon-iran:v1.0
        ports:
        - containerPort: 80
---
# service
apiVersion: v1
kind: Service
metadata:
  name: vuecon-iran-service
spec:
  selector:
    app: vuecon-iran
  type: NodePort
  ports:
  - port: 80
    nodePort: 30080
```
This file creates 2 pods of the sample service and exposes then using a Service. Then apply it:
```sh
# apply the deployment and service
$ kubectl apply -f vuecon-iran-deployment.yml

# query the pods
$ kubectl get pods
NAME                                      READY   STATUS    RESTARTS   AGE
vuecon-iran-deployment-7dbdfb5498-cgq5j   1/1     Running   0          12s
vuecon-iran-deployment-7dbdfb5498-jmzhg   1/1     Running   0          12s

# query services
$ sudo kubectl get services
NAME                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes            ClusterIP   10.43.0.1       <none>        443/TCP          2d11h
vuecon-iran-service   NodePort    10.43.186.193   <none>        80:30080/TCP     4m15s
```
And we can access the app by: `http://k8srv.local:30080`

