# User Management

### Add a user
```sh
$ sudo adduser clloudapps
```

### Add a user in a group
In this example we add user to the sudo group
```sh
$ sudo usermod -aG cloudapps sudo
```
*** Note: Needs logout to take effect ***

### Remove user from a group
```sh
$ sudo deluser cloudapps sudo
```

### Switch between users
```sh
$ su - cloudapps

# check current user
$ whoami
cloudapps

#logout
$ exit
```

### Run a new terminal as a user with sudo privillages
```sh
$ sudo -u cloudapps bash
```
