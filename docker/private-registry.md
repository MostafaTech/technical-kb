# Docker Private Registry

Sources:
* https://oracle-base.com/articles/linux/docker-using-a-local-docker-registry

```sh
# pull the registry image to the master docker
$ docker pull registry

# generate tls key and certificate
$ openssl req -nodes -sha256 -x509 -days 3650 \
  -keyout /home/mostafa/registry/certs/k8srv.local.key \
  -out /home/mostafa/registry/certs/k8srv.local.crt \
  -subj "/CN=k8srv.local/O=K8SRV/L=Tehran/ST=Tehran/C=IR"

# run the registry as a docker container
$ docker run -d \
  -p 5000:443 \
  -v /home/mostafa/registry/images:/var/lib/registry \
  -v /home/mostafa/registry/certs:/certs \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:443 \
  -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/k8srv.local.crt \
  -e REGISTRY_HTTP_TLS_KEY=/certs/k8srv.local.key \
  --restart always
  --name registry \
  registry:latest
```
Copy private registry certificate into master docker certs.d dir if the certificate is self signed
```sh
$ sudo mkdir /etc/docker/certs.d/
$ sudo mkdir /etc/docker/certs.d/k8srv.local:5000
$ sudo cp \
  /home/mostafa/registry/certs/k8srv.local.crt \
  /etc/docker/certs.d/k8srv.local:5000/ca.crt
```
Push a sample image to the registry
```sh
# first pull an image from docker-hub
$ docker pull nginx:alpine
# add a tag to the image with our private registry url as prefix
$ docker tag nginx:alpine k8srv.local:5000/nginx:alpine
# push the image with new tag to the private registry
$ docker push k8srv.local:5000/nginx:alpine
# then we can remove the images from master docker
$ docker rmi nginx:alpine
$ docker rmi k8srv.local:5000/nginx:alpine
```