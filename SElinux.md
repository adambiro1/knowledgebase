view status of SElinux:
```
getenforce
```

turn off SElinux/turn it to permissive mode:
```
setenforce 0
```

turn on SElinux/turn it to enforcing mode:
```
setenforce 1
```

#### File management

use -Z to see SElinux information to file:
```
ls -Z
```
**restorecon** - restore file(s) default SELinux security contexts 

*use after moving files with mv command*

or just use:
```
mv -Z
```

**chcon** - change file SELinux security context
```
chcon -t <selinux content> <file>
```

**semanage** - SELinux Policy Management tool

set default context to whole directory:
```
semanage fcontext -a -t httpd_sys_content_t "/data/student(/.*)?"
```
view content for all files:
```
sudo semanage fcontext -l | less
```

#### networking

view all ports and types managed by SElinux:
```
sudo semanage port -l | less
```

add port:
```
sudo semanage port -a -t ssh_port_t -p tcp 2022
```

list all booleans:
```
sudo getsebool -a | less
```

change boolean:
```
sudo setsebool httpd_enable_homedirs=1
```
use -P option to make the changes persistent:
```
sudo setsebool -P httpd_enable_homedirs=1
```


