# SSH connection to server


generate ssh key:





ssh-keygen -t ed25519 -f ${HOME}/.ssh/name it 






## Set up
get IP address from server

```
hostname -I
```
create config file in .ssh directory on your machine

```
Host server1
     HostName (ip)
     User (username)
     Port 22
     IdentityFile (file where your ssh pub key is stored)
```
 use it to connect to the server
```
ssh server1
```

 Manually append your public key to the remote ssh server's key to authorized_keys file (when on windows powershell)

*do this on server* 
```
vi ~/.ssh/authorized_keys
```
To disable SSH password authentication, SSH in to your server to edit this file as root

```
 sudo vi /etc/ssh/sshd_config
```
into authentication section write:

 **PasswordAuthentication no**

run this command to reload config file

```
sudo systemctl reload sshd 
```

links:

[disable pswd authentication](https://serverpilot.io/docs/how-to-disable-ssh-password-authentication/)

[add sshpub key to server](https://www.simplified.guide/ssh/copy-public-key)

[sshconfig file client](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/)

---

## Managing sshd_config file

Match (user,group,address) statement makes a specific rules for chossen subject/s
always place Match statements at the and of a configfile(sshd_config):
```
Match user testuser1;
PasswordAuthentication yes
```
Display Motd(message of the day)

**PrintMotd yes**

Print last log:

**PrintLastLog yes**

Time to authenticate:

**LoginGraceTime 2m**

Confgure RED (radom early drop) protocol

**MAXStartups 10:30:100**

Deny/allow users/groups from log via ssh ( deny even if the Match permits) it:

**Denyusers testuser1**

**AllowGroups wheel**




---
Check if sshd is running on server
```
ps ax | grep sshd
```
