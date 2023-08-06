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