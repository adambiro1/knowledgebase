# linux-networking

rhel8 

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


## man pages to look

```
man networkmanager
man networkmanager.conf
man nmcli
man nmcli-examples
man nmsettings

```

## linux-networking usefull programs

**ip** - show / manipulate routing, network devices, interfaces and tunnels

**ss** - another utility to investigate sockets *replacement for netstat*

**ethtool** - query or control network driver and hardware settings

specify type:

**ip-route** - routing table management (instead of route)

**ip link** - network device configuration

Show help information about the bridge object:

```
ip link help bridge
```

```
bridge -h
```

Create a bridge named br0:

```
ip link add br0 type bridge
```

Show bridge details:

```
ip -d link show br0
```

Show bridge details in a pretty JSON format:

```
ip -j -p -d link show br0
```

Add interfaces to a bridge:

```
ip link set veth0 master br0
```
**Spanning Tree Protocol** - STP is to prevent a networking loop, which can lead to a traffic storm in the network



enable STP on a bridge:

```
ip link set br0 type bridge stp_state 1
```

show the STP blocking state on the bridge:

```
ip -j -p -d link show br0 | grep root_port
```

```
bridge link show
```

tag vlan

```jsx
ip link add link eth0 name eth0.10 type vlan id 10
```

**tcpdump** - dump traffic on a network


**nc** (netcat) — arbitrary TCP and UDP connections and listens


test if the ports are open on the host

```
nc -zvn <IP address> <portnumber>
```

**curl**


config file: ~/.curlrc

retrieve connection headers:

```
curl -I -v <address>
```

check if proxy is working

```
curl -O -L "https://www.redhat.com/index.html" -x "proxy.example.com:3128"
```

**traceroute** - print the route packets trace to network host

**nmap** - Network exploration tool and security / port scanner


```
nmap <ip address>
```

scan whole range of networks with wildcards:

```
nmap -sn 127.0.0.*
```

scan just certain range:

```
nmap -sn 127.0.0.1-5

```

do a fast scan:

```
nmap -F 127.0.0.1-5

```

put an output in to a file:

```
nmap -oG outputfile -F 127.0.0.1-5

```

more options:

```
nmap scanme.nmap.org -p21 --packet-trace

```

Treat target as it is online:

```
nmap <address> -Pn

```

**hping3** - send (almost) arbitrary TCP/IP packets to network hosts

**wavemon** - a wireless network monitor

**socat** - Multipurpose relay "(SOcket CAT)"

**ipset** — administration tool for IP sets


**iptraf-ng** - Interactive Colorful IP LAN Monitor

**mrtg** - The Multi Router Traffic Grapher (MRTG) is a tool to monitor the traffic load on network links.  MRTG generates HTML pages
containing PNG images which provide a LIVE visual representation of this traffic.

**vnstat** - a console-based network traffic monitor


**bmon** - bandwidth monitor and rate estimator

**stunnel** - TLS offloading and load-balancing proxy

**tshark** - Dump and analyze network traffic *terminal based wireshark, install as wireshark-cli*


show network devices:

```
sudo tshark -D
```

capture:

```
sudo tshark -i <interface>
```

ping ipaddress in process:

```
sudo tshark -i <interface> host <ipaddress>
```

save your output to a file:

```
sudo tshark -w /tmp/nlog.pcap -i <interface>
```

read that file

```
sudo tshark -r /tmp/nlog.pcap
```

**iperf3** - perform network throughput tests

**ifstat** - handy utility to read network interface statistics

**teamdctl** — team daemon control tool

**tracepath** - traces path to a network host discovering MTU along this path

**whois** - client for the whois directory service

**nmstatectl** - A nmstate command line tool

**mtr** - a network diagnostic tool

**mtr-packet** - send and receive network probes

**librenms -** network monitoring tool


**networkmanager** - network management daemon


### Tips network manager

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

change ip address method from dynamic to static:

```
sudo nmcli connection modify enp1s0 ipv4.method manual ipv4.address <adress> ipv4.gateway <address> ipv4.dns <address>

```

show wifi details

```
sudo nmcli device wifi show-password

```

connect  to internet:

```
nmcli connection up <connection name>
```

vLan tag:

```
nmcli connection add type vlan con-name vlan10 ifname vlan10 vlan.parent enp2s0 vlan.id 10
```

bring connection up

```
nmcli connection up vlan10
```

when creating network manager config file place it to: /etc/NetworkManager/conf.d

## Networkd resolved

```
man systemd.network
```

```
networkctl reload
```

view network

```
networkctl list
```

```
networkctl status
```

```
resolvectl
```

### dns

**dig** - DNS lookup utility

check mx record:

```
dig google.com mx

```

digrc file: `+noall +answer`

#### dnssec
**delv** - DNS lookup and validation utility

check dnssec validation chain:

```
delv <domain> aaaa +multi +vtrace
```

check if the record if signed and also check if our resolver supports dnssec:

```
dig @8.8.8.8 www.isc.org A +dnssec +multiline
```

better with delv(tool meant for dnssec validation):

```
delv @8.8.8.8 www.isc.org A +rtrace
```

```
delv @8.8.8.8 www.isc.org A +multiline
```

disable dns flag checkning to be sure that there is not a resolving problem:

```
dig www.dnssec-failed.org A +multiline +cd
```

check the presence of DNSKEY record types:

```
dig @8.8.8.8 caais.gov.cz DNSKEY +multiline  +noall +answer
```

see if your zone data is signed:

```
dig @8.8.8.8 caais.gov.cz SOA +dnssec +multiline
```

check RRSIG and dnskey:

```
dig @8.8.8.8 example.com. DNSKEY +dnssec +cd +multiline
```

check nse3 parameters:

```
dig @ns2.gov.cz caais.gov.cz nsec3param +short
```

**host** - DNS lookup utility

```
host google.com

host -t ns google.com
#or
host -t mx google.com
```

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


## firewalld

administration via:

```
firewall-cmd
```

List all Available services:

```
firewall-cmd --get-services
```

list all allowed services:

```
firewall-cmd --list-services

```

get info about the service:

```
firewall-cmd --info-service=ssh

```

add service:

```
firewall-cmd --add-service=http

```

remove service:

```
firewall-cmd --remove-service=http

```

to make changes persistent add: *--permanent*:

```
firewall-cmd --add-service=http --permanent

```


 Create custom service XML files in /etc/firewalld/services



### zones
Default zones:

**block** Incoming network connections are rejected with an “icmp-host-prohibited” message. Only network connections that were initiated on this system are allowed.

**dmz** For use on computers in the demilitarized zone. Only selected incoming connections are accepted, and limited access to the internal network is allowed.

**drop** Any incoming packets are dropped and there is no reply.

**external** For use on external networks with masquerading (Network Address Translation [NAT]) enabled, used especially on routers. Only selected incoming connections are accepted.

**home** For use with home networks. Most computers on the same network are trusted, and only selected incoming connections are accepted.

**internal** For use in internal networks. Most computers on the same network are trusted, and only selected incoming connections are accepted.

**public** For use in public areas. Other computers in the same network are not trusted, and limited connections are accepted. This is the default zone for all newly created network interfaces.

**trusted** All network connections are accepted.

**work** For use in work areas. Most computers on the same network are trusted, and only selected incoming connections are accepted.

list all zones:

```
firewall-cmd --get-zones

```

list active zones:

```
firewall-cmd --get-active-zones

```

get default zone:

```
firewall-cmd --get-default-zone

```

get information about a zone:

```
firewall-cmd --info-zone=internal

```

add port to default zone:

```
firewall-cmd --add-port=2022/tcp
```

### iptables


List current config:

```
sudo iptables -L
```

```
sudo ip6tables -L
```

Create rule:

```
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

```
sudo iptables -A INPUT -p tcp --dport ssh -j ACCEPT
```

Open tcp and udp whenmaking dns server:

```
sudo iptables -A INPUT -p tcp --dport 53 -j ACCEPT
```

```
sudo iptables -A INPUT -p udp --dport 53 -j ACCEPT
```

Also open loopback:

```
sudo iptables -I INPUT 1 -i lo -j ACCEPT
```

See port numbers instead off nanes:

```
sudo iptables -L -n
```

Use -v option to see the number of packets counted by each rule:

```
sudo iptables -L -v
```

### nftables

**NFTables Utility**

`man nft`

### ntp

check tracking information on the server:

```
chronyc tracking
```

The Reference ID line just tells us the hostname or the IP address of the remote time
server that this local timeserver is synchronized to.


The sources command will show you all of the time servers that our machine can
access:

```
chronyc sources
```

check the machines that are set up for this timeserver:

```
sudo chronyc clients
```

show the number of NTP packets and command packets that were received from
the clients:
