# Kubernetes
As kubernetes has multiple implementions and any one of them has different configurations and service names, some of the specific commands or options described in each implemention file.

## Implementions
* [K3S](./impl-k3s.md)

## Resources
* [Deployments](./res-deployment.md)
* [Services](./res-service.md)
* [Ingress]()

## Basics
* [Labels](./basic-label.md)
* [Annotations](basic-annotation.md)

## Common commands
```sh
# apply a resource or scale deployment
$ kubectl apply -f deployment.yml

# replace resources with new configs
$ kubectl replace --force -f deployment.yml

# delete resources
$ kubectl delete <resource-file>
$ kubectl delete service <service>
$ kubectl delete deployment <deployment>

# get all pods by namespace
$ kubectl get pods -n default
$ kubectl get pods --all-namespaces

# describe
$ kubectl describe pod <pod-name>
$ kubectl describe deployment <deployment-name>
```

## Go into a pod