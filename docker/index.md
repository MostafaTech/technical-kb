# Docker

### Installation
```sh
$ sudo apt-get update

$ sudo apt-get install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"

$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io

# Add the user to the docker group
$ sudo usermod -aG docker ${USER}
```
Installing docker-compose\
*Note: get latest version from: https://github.com/docker/compose/releases*
```sh
$ sudo curl -L \
  https://github.com/docker/compose/releases/download/1.25.5/docker-compose-`uname -s`-`uname -m` \
  -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ docker-compose --version
```

Or if you downloaded docker-compose before, you can copy it
```sh
$ scp docker-compose-Linux-x86_64 docker@192.168.99.101:/home/docker
$ docker-machine ssh
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo mv ./docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
$ docker-compose --version
```

### Use Docker as a non-root user
```sh
$ sudo usermod -aG docker $USER
```

### Common Commands
```sh
# restart the service
$ sudo service docker restart

# access the shell of a container
$ docker exec -it <container-id> bash|sh

# stop all containers
$ docker stop $(docker ps -a -q)
$ docker rm $(docker ps -a -q)
```


### Configuration files
* Service configutaion: `/lib/systemd/system/docker.service`


### Change the http socket port
* open the `/lib/systemd/system/docker.service` file as root user
* change the line `ExecStart=/usr/bin/dockerd -H=fd:// -H=tcp://0.0.0.0:4243` as you wish

