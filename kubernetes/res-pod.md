# POD
A pod is a set of containers running on a node.

## Sample pod yaml file
Create the `busybox-pod.yml` file:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  restartPolicy: Always
  containers:
  - name: busybox
    image: busybox
    command:
    - sleep
    - "3600"
    env:
    - name: DEMO_ENV1
      value: env_value1
    - name: DEMO_ENV2
      value: env_value2
```

Create the pod:
```sh
$ kubectl create -f busybox-pod.yml
$ kubectl get pods -n default
```

go into the pod:
```sh
$ kubectl exec -it busybox -- sh
/# set
DEMO_ENV1='env_value1'
DEMO_ENV2='env_value2'
...
```
