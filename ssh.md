# SSH connection to server

## Set up

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
To disable SSH password authentication, SSH in to your server as root to edit this file 

```
 sudo vi /etc/ssh/sshd_config
```
into authentication section write: **PasswordAuthetication no**

run this command to reload config file

```
sudo systemctl reload sshd 
```

links:

[disable pswd authentication](https://serverpilot.io/docs/how-to-disable-ssh-password-authentication/)

[add sshpub key to server](https://www.simplified.guide/ssh/copy-public-key)

[sshconfig file client](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/)

---