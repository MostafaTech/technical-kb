# Giving access the internet to a container

Sources:
* https://stackoverflow.com/a/45644890/4023416

First thing to check is run cat /etc/resolv.conf in the docker container. If it has an invalid DNS server, such as nameserver 127.0.x.x, then the container will not be able to resolve the domain names into ip addresses, so ping google.com will fail.

Second thing to check is run cat `/etc/resolv.conf` on the host machine. Docker basically copies the host's `/etc/resolv.conf` to the container everytime a container is started. So if the host's `/etc/resolv.conf` is wrong, then so will the docker container.

If you have found that the host's `/etc/resolv.conf` is wrong, then you have 2 options:

1. Hardcode the DNS server in daemon.json. This is easy, but not ideal if you expect the DNS server to change.

2. Fix the hosts's `/etc/resolv.conf`. This is a little trickier, but it is generated dynamically, and you are not hardcoding the DNS server.

### 1. Hardcode DNS server in docker daemon.json

Edit /etc/docker/daemon.json
```json
{
    "dns": ["10.1.2.3", "8.8.8.8"]
}
```
Restart the docker daemon for those changes to take effect:
```sh
sudo systemctl restart docker
```

Now when you run/start a container, docker will populate `/etc/resolv.conf` with the values from daemon.json.

### 2. Fix the hosts's /etc/resolv.conf
Ubuntu 18.04 and later

Ubuntu 18.04 changed to use `systemd-resolved` to generate `/etc/resolv.conf`. Now by default it uses a local DNS cache `127.0.0.53`. That will not work inside a container, so Docker will default to Google's `8.8.8.8` DNS server, which may break for people behind a firewall.

`/etc/resolv.conf` is actually a symlink (`ls -l /etc/resolv.conf`) which points to `/run/systemd/resolve/stub-resolv.conf` (`127.0.0.53`) by default in Ubuntu 18.04.

Just change the symlink to point to `/run/systemd/resolve/resolv.conf`, which lists the real DNS servers:
```sh
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

Verify on the host: `cat /etc/resolv.conf`

Now you should have a valid `/etc/resolv.conf` on the host for docker to copy into the containers.