## change password for user faster
```
sudo echo noveheslo | passwd --stdin testuser
```
View the top 10 most-CPU-consuming processes:
```
ps -L aux | sort -nr -k 3 | head -10
```

View the top 10 most-RAM-consuming processes:
```
ps -L aux | sort -nr -k 4 | head -10
```

List info about device:
```
lspci -s 0:1f.2 -n -v
```

Check CPU load average:
```
cat /proc/loadavg
```

Check opened prots:
```
ss -tulnp --no-header | awk '{print($1, $5, $7)}'
```

```
ss -tulnp
```
```
ss -tulpn | grep 22
```
with netsat:
```
netstat -tulpn
```

change random password for a user and also put it in a file:
```
mkpasswd | tee <file> | passwd --stdin rhel
```

have a resverse history seach *CTRL r*:
```
(reverse-i-search)`gr': dnf grouplist
```


list all available commands:
```
compgen -c
```