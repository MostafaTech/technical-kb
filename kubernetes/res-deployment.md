# Deployments
Define Pods and strategy in one YAML structured file

Deployment -> Replication Controller -> Pods...

## Sample deployment file
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vuecon-iran-deployment
  namespace: default
  labels:
    app: vuecon-iran
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
      - name: vuecon-iran-ui
        image: k8srv.local:5000/vuecon-iran:v1.0
        ports:
        - containerPort: 80
```

Describe the file:
* apiVersion: `apps/v1`, for versions before 1.9.0 use `apps/v1beta2`
* metadata
  * namespace
* spec
  * selector
    * matchLabels: labels of the pods of deployment
  * replicas: tells deployment to run 2 pods matching the template
  * template: a template to create pods from
    * metadata: metadata of a pod
    * spec: specifications of a pod
      * containers: list of containers to run on a pod
        * name: name of the container
        * image: <name>:<tag> of the docker image of the container
        * ports: list of exposed ports
          * name: the name of the port to reference later
          * containerPort: exposed port of the container
        * imagePullPolicy: Default `Always`
          * Always: Always pull images from registry
          * Never: Never pull images from registry. only use local images

## Commands
Create a deployment
```sh
$ kubectl create -f deployment.yml
# OR
$ kubectl apply -f deployment.yml
```

*Note 1: If you run the above command again on a created deployment, i will restart the pods*

*Note 2: To scale up or down replicas run the above command again*

Scale the deployments by cli
```sh
$ kubectl scale deployment <deployment-name> --replicas=<new-number-of-replicas>
```

To pull the container images again
```sh
$ kubectl replace --force -f deployment.yml
```

To Delete the deployment
```sh
$ kubectl delete deployment <deployment-name>
```