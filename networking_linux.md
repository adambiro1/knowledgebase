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

**nc** (netcat) — arbitrary TCP and UDP connections and listens

**socat** - Multipurpose relay "(SOcket CAT)"

**ipset** — administration tool for IP sets

**iptraf-ng** - Interactive Colorful IP LAN Monitor

**mrtg** - The Multi Router Traffic Grapher (MRTG) is a tool to monitor the traffic load on network links.  MRTG generates HTML pages
       containing PNG images which provide a LIVE visual representation of this traffic.

**vnstat** - a console-based network traffic monitor

[vnstat page](https://humdi.net/vnstat/)

**bmon** - bandwidth monitor and rate estimator

**stunnel** - TLS offloading and load-balancing proxy

**tshark** - Dump and analyze network traffic *terminal based wireshark, install as wireshark-cli*

**iperf3** - perform network throughput tests

**ifstat** - handy utility to read network interface statistics

**ethtool** - query or control network driver and hardware settings

**teamdctl** — team daemon control tool

**traceroute** - print the route packets trace to network host

**tracepath** - traces path to a network host discovering MTU along this path

**dig** - DNS lookup utility

use dig tocheck mx record:
```
dig google.com mx
```

**delv** - DNS lookup and validation utility

**host** - DNS lookup utility


**whois** - client for the whois directory service


**nmstatectl** - A nmstate command line tool

[nmstate](https://nmstate.io/)

[github](https://github.com/nmstate/nmstate)

**NetworkManager** - network management daemon

[networkmanager](https://networkmanager.dev/)

[manual](https://developer-old.gnome.org/NetworkManager/stable/nmcli.html)

**mtr** - a network diagnostic tool

**mtr-packet** - send and receive network probes

[mtr page](https://www.bitwizard.nl/mtr/)

## Firewalld

administration via:
```
firewall-cmd 
```
[firewalld docs](https://firewalld.org/documentation/)



## Tips network manager

show connection details with network manager:
```
sudo nmcli connection show enp1s0
```
find ip4 address:
```
sudo nmcli connection show enp1s0 | grep -i ip4
```
find if the ip is dynamic or static:

```
sudo nmcli connection show enp1s0 | grep -i  method
```
change ip address method from dynamci to static:

```
sudo nmcli connection modify enp1s0 ipv4.method manual ipv4.address <adress> ipv4.gateway <address> ipv4.dns <address>
```
show wifi details

```
sudo nmcli device wifi show-password
```

when creating network manager confi file place it to: /etc/NetworkManager/conf.d



## DNS

set your DNS:

/etc/resolv.conf
```
# IPv4 dns
nameserver 1.1.1.1
nameserver 8.8.8.8
# IPv6 dns
nameserver 2606:4700:4700::1111
```
you can have max 3 entries

to make it permanent also change the entries with nmcli like in above examples


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


