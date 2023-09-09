**smartctl** - Control and Monitor Utility for SMART Disks

[smartmontools page](https://www.smartmontools.org/wiki/TocDoc)
```
dnf install smartmontools
```

**dd** - convert and copy a file
```
dd if= of=
```
**df** - report file system space usage

**du** - estimate file space usage

show partitions:
```
cat /proc/partitions
```

**fdisk** - manipulate disk partition table

after using fdisk user partprobe to inform kernel

**partprobe** - inform the OS of partition table changes

**parted** - a partition manipulation program


----
#### LVM

**pvs** — Display information about physical volumes

create physical volume:
**pvcreate** — Initialize physical volume(s) for use by LVM
```
sudo pvcreate /dev/vdb1
```

**vgs** — Display information about volume groups

**vgextend** — Add physical volumes to a volume group
```
vgextend /dev/rhel /dev/vdb1
```

**lvs** — Display information about logical volumes

**lvcreate** — Create a logical volume
```
sudo lvcreate -n test -L 5G rhel
```
**lvextend** — Add space to a logical volume
```
lvextend vg01/lvol01 /dev/sdk3
```


#### XFS

create xfs file system:
```
sudo mkfs.xfs /dev/rhel/test
```


