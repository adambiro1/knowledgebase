# Add sudoers

## CentOSstream

log in as a root 
```
usermod -aG wheel <username>
```

check visudo if the: **%wheel  ALL=(ALL)  ALL** is uncomented

## Ubuntu

```
usermod -aG sudo <username>
```

logs for sudo are in: /var/log/secure