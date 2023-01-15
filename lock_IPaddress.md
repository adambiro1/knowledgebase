# Lock IP Addres on CentOsStream and Alma Linux

create a  /etc/sysconfig/network-scripts/ifcfg-eth0 file

enter there:
```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
PREFIX=24
IPADDR=(ip address)
```
then restart service:
```
sudo systemctl restart NetworkManager.service
```
but this method is depricated, now Network manager stores keyfiles in

*/etc/NetworkManager/system-connections/*

use:
```
 sudo nmcli connection migrate
```

This command migrates all profiles from ifcfg format to keyfile
format and stores them in /etc/NetworkManager/system-connections/

Keys files with your setting is:

*System\ eth0.nmconnection*

