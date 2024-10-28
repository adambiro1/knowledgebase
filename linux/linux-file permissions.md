# linux-file permissions

**Discretionary Access Control DAC**

show permissions on all files in dir:

```
stat -c '%n %a '  *
```

**umask** - permissions for new files


0 – no permissions are blocked (read, write, and execute)

1 – execute permission is blocked

2 – write permission is blocked

3 – write and execute permissions are blocked

4 – read permission is blocked

5 – read and execute permissions are blocked

6 – read and write permissions are blocked

7 – all permissions are blocked (neither read, write, nor execute)

### Advanced Permissions

>To apply SUID, SGID, and sticky bit, you can use chmod as well. SUID has numeric value 4, SGID has numeric value 2, and sticky bit has numeric value 1.


Finding spurious SUID or SGID files:

```
sudo find / -type f \( -perm -4000 -o -perm -2000 \) > suid_sgid_files.txt
```

You can prevent SUID and SGID usage on a partition by mounting it with the nosuid option in /etc/fstab.

apply SGID:

```
chmod 2755 /somedir
```

apply sticky bit

```
chmod 32755 /somedir
```

relative mode:

For SUID, use chmod u+s
For SGID, use chmod g+s
For sticky bit, use chmod +t  followed by the name of the file or the directory
that you want to set the permissions on

Permission Numeric Value RelativeValue  On Files                                      On Directories

SUID           4                      u+s     User executes file with permissions of file owner. Nomeaning.

SGID           2                      g+s     User executes file with permissions of group owner. Files created in
directory get the same
group owner.

Sticky bit     1                      +t        No meaning.      Prevents users from deleting files from other users.

### User-Extended Attributes

**lsattr** - list file attributes on a Linux second extended file system

**chattr** - change file attributes on a Linux file system

add atribute:

```
chattr +s somefile
```

remove attribute:

```
chattr -s somefile
```

**A** This attribute ensures that the file access time of the file is not modified.
Normally, every time a file is opened, the file access time must be written to
the file’s metadata. This affects performance in a negative way; therefore, on
files that are accessed on a regular basis, the A attribute can be used to disable
this feature.

**a** This attribute allows a file to be added to but not to be removed.

**c** If you are using a file system where volume-level compression is supported,
this file attribute makes sure that the file is compressed the first time the com-
pression engine becomes active.

**D** This attribute makes sure that changes to files are written to disk
immediately, and not to cache first. This is a useful attribute on important database files to make sure that they do not get lost between file cache and hard disk. 

**d** This attribute makes sure the file is not backed up in backups where the legacy dump utility is used.

**I** This attribute enables indexing for the directory where it is enabled.

**i** This attribute makes the file immutable. Therefore, no changes can
be made to the file at all, which is useful for files that need a bit of extra protection.

**s** This attribute overwrites the blocks where the file was stored with 0s after the file has been deleted. This makes sure that recovery of the file is not possible after it has been deleted.

**u** This attribute saves undelete information. This allows a utility to be developed that works with that information to salvage deleted files.

### Access Control Lists

before setting acl remove all permissions for other user (600)

access rights for files and directories

```
man acl
```

**getfacl** - get file access control lists

 

```
getfacl /dir
```

**setfacl** - set file access control lists

```
setfacl -m g:sales:rx /dir
```

```
setfacl -m u:test1:r acl_demo.txt
```


If you want to use ACLs to configure access for multiple users or groups to the same directory, you have to set ACLs twice. First, use `setfacl -R -m` to modify the ACLs for current files. Then, use setfacl -m d: to take care of all new items that will be created also.


if you want group sales to have read and execute permissions on everything that will ever be created in the /data directory (d: before is important):

```
setfacl -m d:g:sales:rx /data
```

get permissions on anything that is created in /data:

```
setfacl -m d:o::- /data
```

Removing a specific permission by using an ACL mask:

remove:

```
setfacl -x u:test1 acl_demo.txt
```

```
setfacl -x g:accounting acl_demo.txt
```

mask:

```
setfacl -m m::r acl_demo.txt
```

others are still there:

```
# file: acl_demo.txt
# owner: adam
# group: adam
user::rw-
user:test1:rwx                  #effective:r--
group::---
mask::r--
other::---
```

create the backup:

```
getfacl -R /directory > file.acls
```

restore settings from backup file:

```
setfacl --restore=file.acls
```

### **Using the tar --acls option to prevent the loss of ACLs during a backup**

```
tar cJvf new_perm_dir_backup.tar.xz new_perm_dir/ --acls
```


The presence of the + signs indicates that the ACLs did survive the backup-and-restore procedure. The one slightly tricky part about this is that you must use `--acls` for both the backup and the restoration. If you omit the option either time, you will lose your ACLs.
