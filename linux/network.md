# Linux Network

### commands
```sh
# see network adapters
$ ifconfig
$ ip address
$ ip link
```

### Set static ip
Ubuntu 18.04 uses netplan to config network:\
Edit the `/etc/netplan/50-cloud-init.yaml` file.
```yaml
network:
    ethernets:
        enp0s3:
            dhcp4: false
            addresses:
            - 192.168.56.110/24
#            gateway4: 192.168.56.1
        enp0s8:
            dhcp4: true
            nameservers:
                addresses:
                - 185.55.226.26
                - 185.55.225.25
    version: 2
```

* Note 1: You should edit this file as root
* Note 2: only define gateway4 on the adapter that connected to the internet

Then apply the configuration
```sh
$ sudo netplan apply
```
