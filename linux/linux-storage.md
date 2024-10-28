# linux-storage


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

**lsblk** - list block devices

show also file system information:

```
lsblk -f
```

**fdisk** - manipulate disk partition table

after using fdisk user partprobe to inform kernel

**partprobe** - inform the OS of partition table changes

**gdisk** - Interactive GUID partition table (GPT) manipulator

delete all existing partiotions an a disk:

```
wipefs -a <PhysicalVolume>`
```

**parted** - a partition manipulation program

1. parted /dev/sdb
2. help
3. print
4. mklabel (click tab twice for options) choose gpt
5. mkpart (type part1 it does not matter that much)
6. choose file system(it does not matter you will change it afterwards but choose xfs)
7. Start? 1Mib
8. End? 1Gib
9. quit

after quitting parted do mkfs.xfs /dev/sdb1


## Adding Swap Partitions

check swap:

```
cat /proc/swaps
```


1. `gdisk /dev/sdb`
2. n (create 1GiB)
3. t (choose 8200)
4. w and exit
5. `mkswap /dev/sdb1` (on a number your created it)
6. check amount of swap space: `free -m`
7. `swapon /dev/sdb1` (to activate that swap you created)
8. check amount of swap space: `free -m` (new swap should be there)
9. to /etc/fstab add : `/dev/sdb1 none swap defaults 0 0`

## Adding Swap Files

1. `dd if=/dev/zero of=/swapfile bs=1M count=100`  (The result is a 100-MiB file)
2. `mkswap /swapfile`
3. `swapon /swapfile`
4. /etc/fstab : `/swapfile none swap defaults 0 0`


Verifies /etc/fstab syntax and alerts you if anything is incorrect:

```
findmnt --verify
```

Mounts all file systems that have a line in /etc/fstab and are not currently mounted:

```
mount -a
```

---

### LVM


**pvs** — Display information about physical volumes

**pvdisplay** - Display various attributes of physical volume(s)

create physical volume:
**pvcreate** — Initialize physical volume(s) for use by LVM

```
sudo pvcreate /dev/sdb1

```

**pvscan** - List all physical volumes scans all supported LVM block devices in the system for physical volumes. 

remove physical volume:

```
pvremove "device"
```

### volume groups

**vgs** — Display information about volume groups

**vgdisplay** - Display volume group information

**vgscan** - Search for all volume groups

**vgcreate** create a volume group:

```
vgcreate vgdata /dev/sdb1
```

create it in one go by defining whole device in command skipping pvcreate:

```
vgcreate vgdata /dev/sdb1
```

**vgextend** — Add physical volumes to a volume group

```
vgextend myvg 'device'
```

Rename an existing volume group:

```
vgrename myvg myvg1
```

**vgmerge** - Merge volume groups

check man vgmerge

**removing physical volumes from a volume group**


**vgreduce** — Remove physical volume from a volume group 

If the physical volume is still being used, migrate the data to another physical volume from the same volume group:

```
pvmove "old device"
```

if there is not enough space on other devices add new one and move it there:

```
pvcreate"new dev"
```

```
vgextend myvg "new dev"
```

```
pvmove "old dev" "new dev"
```

```
vgreduce myvg "device"
```

remove physical volume:

```
vgreduce myvg "old device"
```

verify with pvs

**split volume groups**

Split the existing volume group *myvg* to the new volume group *yourvg:*

```
vgsplit myvg yourvg "device"
```


### logical volumes


**lvs** — Display information about logical volumes


>lv’s are in /dev/mapper/


**lvscan** — List all logical volumes in all volume groups

display info about volume

```
lvdisplay -v /dev/myvg/mylv
```

**lvcreate** — Create a logical volume

```
lvcreate -n lvdata -l 50%FREE vgdata
```

create a file system on top of lv:

```
mkfs.ext4 /dev/vgdata/lvdata
```

make a dir where lv can be mounted:

```
mkdir /files
```

Add the following line to the bottom of /etc/fstab:

```
/dev/vgdata/lvdata /files ext4 defaults 0 0
```

remount stuff in /etc/fstab:

```
mount -a
```

check if everything is allright with /etc/fstab

```
findtmnt --verify
```

check wit lsblk that partition was mounted succesfully


### resizing LVM


make sure you have a disk to add, then add it:

```
vgextend vgdata /dev/sdd2
```

```
vgs  #verify that physical volume has been added
```

```
lvs  #check current size of lv lvdata
```

```
df -h  #check current size ov lv lvdata
```

extend lv:

```
lvextend -r -l +50%FREE /dev/vgdata/lvdata
```

check lvs and df -h again if changes we applied

## XFS

create xfs filesystem:


```
sudo mkfs.xfs /dev/sdb1
```

or

```
mkfs -t xfs /dev/sdb1
```


**xfs_admin** - change parameters of an XFS filesystem



### Stratis

https://www.redhat.com/en/blog/stratis-managed-file-systems-microsoft-sql-server-rhel?blaid=5564091

## Raid

[https://docs.oracle.com/en/operating-systems/oracle-linux/8/stordev/stordev-WorkingWithSoftwareRAID.html#topic_vf4_33m_zzb](https://docs.oracle.com/en/operating-systems/oracle-linux/8/stordev/stordev-WorkingWithSoftwareRAID.html#topic_vf4_33m_zzb)

[https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/managing_storage_devices/managing-raid_managing-storage-devices#creating-a-software-raid-on-an-installed-system_managing-raid](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/managing_storage_devices/managing-raid_managing-storage-devices#creating-a-software-raid-on-an-installed-system_managing-raid)

### software raid 

`man mdadm`
