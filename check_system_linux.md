# Tools for checking system status/logs...

**dmesg** - print or control the kernel ring buffer

**logger** - enter messages into the system log

**auditd** - The Linux Audit daemon

Logs are stored in /var/log

View all logs from wished day:

```
grep ‘Aug 31 18:42:54’ /var/log/messages
```

Change log rules in: */etc/rsyslog.conf*

Log rotation: */etc/logrotate.conf*


