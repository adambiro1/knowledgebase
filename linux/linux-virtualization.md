# linux-virtualization


### check if your set up is correct

```
virt-host-validate
```


**install redhat via commandline with out grapical interface:**

```
sudo virt-install \
 --name rhel-http-sever --memory 2048 \
 --vcpus 1 --disk size=60 --os-variant rhel9.2 \
 --cdrom /home/user/Downloads/iso/rhel-9.2-x86_64-dvd.iso \
 --graphics none --extra-args='console=ttyS0'
```

## get info about

**vm:**

```
sudo virsh dominfo rhel-http-server
```

**from xml file:**

```
sudo virsh dumpxml rhel-http-server
```

**disks:**

```
sudo virsh domblklist rhel-http-server
```

**file system:**

```
sudo virsh domfsinfo rhel-http-server
```

**cpu:**

```
sudo virsh vcpuinfo rhel-http-server
```

### save VM state and restore it where it was:


```
sudo virsh managedsave rhel-http-server
```

list saved machines:

```
sudo virsh list --managed-save --all
```

start it again where it left:

```
sudo virsh start rhel-http-server
```

### networking

**network interfaces:**

```
sudo virsh net-list
```

**specific interface**

```
sudo virsh net-info default
```


**Making VM accessible to other devices**


### create bridge for machines


```
nmcli con show
nmcli device show
virsh net-list --all
nmcli con add ifname br0 type bridge con-name br0
nmcli con add type bridge-slave ifname eno1 master br0
nmcli con show
vim bridge.sh
ls
sh ./bridge.sh
nmcli con show
nmcli con show --active
virsh net-list --all
vim bridge.xml
virsh net-define ./bridge.xml
virsh net-start br0
virsh net-autostart br0
virsh net-list --all
```

Remove VM:

```
sudo virsh undefine <domain name> --remove-all-storage --snapshots-metadata
```

## storage

change pool 


after changing pool you need to give permissions to qemu user to access storage pool in you Home dir


do not forget to do it recursive:

```
sudo setfacl -R -m u:qemu:rx /home/user/
```

## Snapshot

create a snapshot:

```
sudo virsh snapshot-create-as --domain <virtname> --name <snapshotname> --description "vanilla after install and 1. update"
```

revert snapshot:

```
sudo virsh snapshot-revert --domain rhel8-9 rhel8-9_clean
```