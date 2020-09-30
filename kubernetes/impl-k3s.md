# K3S Implemention of Kubernetes

## Installation


## Service
```sh
# restart service
$ sudo systemctl restart k3s
```

## Change registry mirrors to private
Sources:
* https://rancher.com/docs/k3s/latest/en/installation/private-registry

Create the file `/etc/rancher/k3s/registries.yaml`
```yaml
mirrors:
  "k8srv.local:5000":
    endpoint:
      - "https://k8srv.local:5000"
configs:
  "k8srv.local:5000":
    tls:
      cert_file: /home/mostafa/registry/certs/k8srv.local.crt
      key_file: /home/mostafa/registry/certs/k8srv.local.key
      ca_file: /home/mostafa/registry/certs/k8srv.local.crt
```
*Note: if we have a self signed certificate, the cert_file and ca_file should be same*


## Configuration files and locations
* Certificates dir:  `/var/lib/rancher/k3s/server/tls`
* Registries mirrors: `/etc/rancher/k3s/registries.yaml`

