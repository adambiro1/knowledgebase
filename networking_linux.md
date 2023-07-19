# Networking

## man pages to look
```
man networkmanager
man networkmanager.conf
man nmcli
man nmcli-examples
man nmsettings
```

## Usefull programs

**ip** - show / manipulate routing, network devices, interfaces and tunnels

**ss** - another utility to investigate sockets *replacement for netstat*

**tcpdump** - dump traffic on a networ

**nmap** - Network exploration tool and security / port scanner

**socat** - Multipurpose relay "(SOcket CAT)"

**ipset** — administration tool for IP sets

**iptraf-ng** - Interactive Colorful IP LAN Monitor

**mrtg** - The Multi Router Traffic Grapher (MRTG) is a tool to monitor the traffic load on network links.  MRTG generates HTML pages
       containing PNG images which provide a LIVE visual representation of this traffic.

**stunnel** - TLS offloading and load-balancing proxy

**tshark** - Dump and analyze network traffic *terminal based wireshark, install as wireshark-cli*

**iperf3** - perform network throughput tests

**ifstat** - handy utility to read network interface statistics

**ethtool** - query or control network driver and hardware settings

**teamdctl** — team daemon control tool

**traceroute** - print the route packets trace to network host

**tracepath** - traces path to a network host discovering MTU along this path

**dig** - DNS lookup utility

**whois** - client for the whois directory service





## Tips

when creating network manager confi file place it to: /etc/NetworkManager/conf.d



## Older depricated method before CentOSsteam9/Rhel9...

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

Keys files in CentOSStream9 with your setting is:

*System\ eth0.nmconnection*


