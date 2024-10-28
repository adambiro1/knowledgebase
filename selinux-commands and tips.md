# selinux commands and tips

config file:

```
vi /etc/selinux/config
```

install selinux tools:

```
sudo dnf install setools policycoreutils policycoreutils-python-utils
```

```
sudo dnf install setroubleshoot
```

then restart selinux service:

```
sudo service auditd restart
```

Install man pages for selinux policy:(on rhel9 they are not there by default)

```
dnf install selinux-policy-doc
```

update man pages

search for selinux context:

```
man -k _selinux | grep http
```

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

get detailed information about the current protection status(use -v option for better detail):

```
sestatus -v
```

### [File management](https://github.com/adambiro1/knowledgebase/blob/main/SElinux.md#file-management)

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

**semanage** - SELinux Policy Management tool

set this context type to any new directory that you want to use as the DocumentRoot:

```
semanage fcontext -a -t httpd_sys_content_t "/mydir(/.*)?"
```

set default context to whole directory:

```
semanage fcontext -a -t httpd_sys_content_t "/data/student(/.*)?"
```

write the context also to file system:

```
restorecon -R -v mydir
```

or create /.autorelabel file that by next boot up updates selinux context for all files

view content for all files:

```
sudo semanage fcontext -l | less
```

### selinux-networking

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

**logging**

Get SElinux log messages from audit log

```
grep AVC /var/log/audit/audit.log
```

Use Sealert to get easier to understand message:

```
journalctl | grep sealert
```

<aside>
💡 To get more details, you should run the command that is suggested. This will get information from the SELinux event database, including suggestions on how to fix the problem.

</aside>

To better analyze what sealert shows use setroubleshoot-server:

```
dnf install setroubleshoot-server
```

install seinfo:

```
dnf install setools-console
```

### troubleshooting

view what actions SELinux denies:

```
ausearch -m AVC,USER_AVC,SELINUX_ERR,USER_SELINUX_ERR -ts today
```

check messages provided by the systemd Journal:

```
journalctl -t setroubleshoot
```

with the setroubleshoot-server package installed:

```
grep "SELinux is preventing" /var/log/messages
```

If SELinux is active and the Audit daemon (auditd) is not running:

```
dmesg | grep -i -e type=1300 -e type=1400
```

temporarily disable dontaudit rules, allowing all denials to be logged:

```
semodule -DB
```

After re-running denied scenario and finding denial messages using the previous steps, the following command enables dontaudit rules in the policy again:

```
semodule -B
```

**sealert** - setroubleshoot client tool 

show all alerts and list more details about selinux problem:

```
sealert -l "*"
```

If the output obtained in the previous step does not contain clear suggestions enable full-path auditing to see full paths to accessed objects and to make additional Linux Audit event fields visible:

```
auditctl -w /etc/shadow -p w -k shadow-write
```

Clear the setroubleshoot cache:

```
rm -f /var/lib/setroubleshoot/setroubleshoot.xml
```

After you finish the process, disable full-path auditing:

```
auditctl -W /etc/shadow -p w -k shadow-write
```