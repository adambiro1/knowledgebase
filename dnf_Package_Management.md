# Working with dnf package managemet

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

use module to install exact version of the package:
```
sudo module install nginx:1.22
```