# Labels

Labels are key/value pairs and can be assigned to any resource in kubernetes.\

Add labels in yaml file:
```yaml
metadata:
  labels:
    key1: value1
    key2: value2
```

## Example 1
Add a label to a node and select by selector

Add the label:
```sh
$ kubectl label nodes master disktype=ssd
```

Run a pod only on nodes with ssd disk type:
```yaml
kind: Pod
metadata: ...
spec:
  containers: ...
  nodeSelector:
    disktype=ssd
```
*Note: You can use disktype!=ssd to run pods on nodes with other than ssd disktype*

