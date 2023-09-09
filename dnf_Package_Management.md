# Working with dnf package managemet

```
man dnf
```

Finds  the  packages  providing  the  given specs:
```
dnf whatprovides dig
```

update only security pathces:
```
dnf update --security
```

download update to cache:
```

dnf update --downloadonly
```
use module to install exact version of the package:
```
sudo module install nginx:1.22
```
find all files asociated with package:
```
dnf repoquery -l ngingx
```

#### dnf groups

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

