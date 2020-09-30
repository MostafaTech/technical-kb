# Openshift

## Minishift
```sh
# starting an openshift cluster:
$ minishift start --no-proxy 192.168.x.x

# restart openshift cluster
$ minishift openshift restart

# add oc to env
$ eval $(minishift oc-env)

# login to system:admin
$ oc login -u system -p admin
```
