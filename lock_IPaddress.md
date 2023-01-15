# Lock IP Addres on CentOsStream

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