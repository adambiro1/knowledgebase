# dnf and rpm package management

```
man dnf
```

## dnf groups

list groups:

```
dnf grouplist
```

list hidden groups:

```
dnf grouplist hidden
```

get information about group

```
dnf groupinfo "group name"
```

install group

```
dnf groupinstall "group name"
```

List installed GPG keys:

```
grep -r gpgkey /etc/yum.repos.d/* /etc/dnf/dnf.conf
```

check for CVE :critical vulnerability exploit (format of cveCVE-2023-43422)

```
dnf check-update --cve <cve identifier>
```

check what will change:

```
dnf check-update --cve <cve identi> --changelogs
```

update the cve:

```
dnf update --cve <cve identi>
```

mount repo from offline cd installation:

```
mkdir /mnt/cdrom
mount /dev/sr0 /mnt/cdrom/
cp /mnt/cdrom/media.repo /etc/yum.repos.d/
vi /etc/yum.repos.d/media.repo
ls -la /mnt/cdrom/
yum repolist
yum makecache
vi /etc/yum.repos.d/media.repo
yum makecache
vi /etc/yum.repos.d/media.repo
yum makecache
yum info haproxy
```

create add that repo:

```
[InstallMedia-BaseOS-RHEL-8.9]
name=Red Hat Enterprise Linux 8.9.0 - BaseOS
gpgcheck=0
cost=500
baseurl=file:///mnt/cdrom/BaseOS
enabled = 1

[InstallMedia-AppStream-RHEL-8.9]
name=Red Hat Enterprise Linux 8.9.0 - AppStream
gpgcheck=0
cost=500
baseurl=file:///mnt/cdrom/AppStream
enabled = 1
```

## rpm

`rpm -qf` Uses filename as its argument to find

the specific RPM package a file belongs to.

`rpm -ql` Uses the RPM database to provide a list of files in the RPM package.

`rpm -qi` Uses the RPM database to provide package information (equivalent to yum info).

`rpm -qd` Uses the RPM database to show all documentation that is available in the package.

`rpm -qc` Uses the RPM database to show all configuration files that are available in the package.

`rpm -q` --scripts Uses the RPM database to show scripts that are used in the package. This is particularly useful if combined with the -p option.

`rpm -qp <pkg>` The -p option is used with all the previously listed options to query individual RPM package files instead of the RPM package database. Using this option before installation helps you find out what is actually in the package before it is installed.

`rpm -qR` Shows dependencies for a specific package.

`rpm -V `Shows which parts of a specific package have been changed since installation.

`rpm -Va` Verifies all installed packages and shows which parts of the package have been changed since installation. This is an easy and convenient way to do a package integrity check.

`rpm -qa `Lists all packages that are installed on this server.