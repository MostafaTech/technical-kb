# Linux (Ubuntu 18.04 +)

* [Network](./network.md)


### Useful commands
```sh
# remove a dir and all of its contents
$ rm -rf dir1

# change permissions of a directory and all of its contents
$ chmod -R 770 .

# free up unused memory
$ sudo sync && sudo sysctl -w vm.drop_caches=3
```