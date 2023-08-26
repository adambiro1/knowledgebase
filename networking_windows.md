# Networking on Windows

## Windows networking commands:

**Ping**

**Tracert** - identifies the route a packet takes between your computer and the destination computer specified in the command

**Pathping** - Provides information about network latency and network loss at intermediate hops between a source and destination.

**Ipconfig** - command-line utility that you can use to trace the path that an Internet Protocol (IP) packet takes to its destination

**ARP** - Displays and modifies the IP-to-Physical address translation tables used by

address resolution protocol (ARP)   arp -a (list mac addresses)

**Getmac** - This tool enables an administrator to display the MAC address for network adapters on a system.
 
**Netstat** - Displays active TCP connections, ports on which the computer is listening, Ethernet statistics, the IP routing table, IPv4 statistics (for the IP, ICMP, TCP, and UDP protocols), and IPv6 statistics (for the IPv6, ICMPv6, TCP over IPv6, and UDP over IPv6 protocols). Used without parameters, this command displays active TCP connections.
```
Netstat -n    do not resolve names only ip addresses

Netstat -a    show also ports that are listening

Netstat -b   shows on which program is using connection

Netstat -f   shows fully qualified domain name
```

**Route** - Manipulates network routing tables

**nslookup**(windows utility) -nslookup - query Internet name servers interactively

check MX record with nslookup:
```
nslookup -debug -type=mx google.com
#or
nslookup -type=MX google.com
#or
nslookup -query=mx google.com

```
find all of the available DNS records of a domain:
```
nslookup -type=any <address>
```
**Net**

**Netuser**

**Netsh** - command-line scripting utility that allows you to, either locally or remotely, display or modify the network configuration of a currently running computer

open netsh shell:
```
netsh
```

show defined aliases:
```
netsh show alias
```

show multicast joins:
```
netsh interface ip show joins
```

reset winsock:
```
netsh winsock reset catalog
```

reset tcp/ip stack:
```
netsh int ip reset reset.log
```

#### interfaces:

show interfaces:
```
netsh interface show interface
```

show index numbers of all interfaces:
```
netsh interface ip show interfaces
```

Configure Specific Network Interface:
```
netsh interface ipv4 set address "<interface name>" static <IP address> <subnet mask> <default gateway>
```

change ip address for n interface:
```
netsh int ip set address "<interface name>" static 192.168.29.101 255.255.255.0 192.168.29.254 1
```

add a primaty DNS server:
```
netsh interface ip add dns name="Connection" addr=<address>
```

#### wireless:

show all wirelesss interfaces:
```
netsh wlan show interfaces
```

show wifi profiles:
```
netsh wlan show profiles
```

show wifi password:
```
netsh wlan show profile name="<profile name>" key=clear
```

check all available wireless networks:
```
netsh wlan show networks
```

check strength of all wifi networks:
```
netsh wlan show networks mode=bssid
```

disconnect form connected wireless device:
```
netsh wlan disconnect
```

connect to available wireless device:
```
netsh wlan connect name="<name>"
```

show drivers of wireless interfaces:
```
netsh wlan show drivers
```

#### check global parameters:
tcp:
```
netsh interface tcp show global
```

udp:
```
netsh interface udp show global
```

disable global parameters for tcp:
```
netsh interface tcp set global rss=disabled
```

enable global parameters for tcp:
```
netsh interface tcp set global rss=enabled
```


#### firewall managemet:

check all firewall rules:
```
netsh advfirewall firewall show rule name=all
```

show firewall rules for current profile:
```
netsh advfirewall show currentprofile
```

allow port to windows firewall:
```
netsh advfirewall firewall add rule name="Open Remote Desktop" protocol=TCP dir=in localport=3389 action=allow
```

allow ping requests from windows firewall:
```
netsh advfirewall firewall add rule name="All ICMP V4" dir=in action=allow protocol=icmpv4
```

block ping requests from windows firewall:
```
netsh advfirewall firewall add rule name="All ICMP V4" dir=in action=block protocol=icmpv4
```

disable windows firewall in all profiles:
```
netsh advfirewall set allprofiles state off
```

reset windows firewall settings to default:
```
netsh advfirewall reset
```

#### proxy settings:

check current proxy settings:
```
netsh winhttp show proxy
```

set proxy:
```
netsh winhttp set proxy "myproxy.proxyaddress.com:8484" "<local>;*.proxyaddress.com"
```

#### Packet Capture:

start packet capture:
```
netsh trace start capture=yes tracefile=c:\trace.etl persistent=yes maxsize=4096
```

stop packet capture:
```
netsh trace stop
```

[packet catupre](https://learn.microsoft.com/en-us/windows/win32/ndf/using-netsh-to-manage-traces)

[use WPA to analyze ETL files](https://learn.microsoft.com/en-us/windows-hardware/test/wpt/opening-and-analyzing-etl-files-in-wpa)



## Powershell:

*Sometimes for better view use | format-list*

*User object for better statistics(click tab for properties)*

Test-netconnection:

(ping)


also specify hops:
```
Test-NetConnection -ComputerName www.google.com -Hops 5
```

```
$test = Test-NetConnection google.com -InformationLevel "Detailed"

$test.PingReplyDetails

$test.PingReplyDetails.Buffer.Length
```

list ip configuration:
```
Get-NetIPConfiguration
```

list all Network Adapters:
```
$netadapters = Get-NetAdapter

$netadapters.MacAddress
```
 
Ipconfig:
 
```
$ipinfo = Get-NetIPConfiguration

$ipinfo[0].IPv4Address
```


```
Get-NetAdapter
```

get a spesific network adapter by name:
```
Get-NetAdapter -Name *Ethernet*
```

get more information VLAN ID, Speed, Connection status:
```
Get-NetAdapter | ft Name, Status, Linkspeed, VlanID
```

get driver information:
```
Get-NetAdapter | ft Name, DriverName, DriverVersion, DriverInformation, DriverFileName
```

get adapter hardware information:
```
Get-NetAdapterHardwareInfo
```

disable and Enable a Network Adapter:
```
Disable-NetAdapter -Name "<name>"
Enable-NetAdapter -Name "name"
```

get IP and DNS address information:
```
Get-NetAdapter -Name "Local Area Connection" | Get-NetIPAddress
```

tracert with PowerShell:


```
$test = Test-NetConnection google.com -TraceRoute

$test.RemoteAddress

$test.TraceRoute , $test.TraceRoute[1]
```


```
Test-NetConnection www.google.com –TraceRoute
```

check opened ports:

(port scanning)

```
Test-NetConnection google.com -Port 80
```
 

Oneliner:
 
```
$ports = 22,80

$address = "google.com"
 
$ports | ForEach-Object { $port = $PSItem; if(Test-NetConnection $address -Port $port -InformationLevel Quiet -WarningAction SilentlyContinue) {Write-Host "Port $port is open" } else { Write-Host "Port $port is closed" } }
```

check dns *nslookup in cmd*:

Resolve-DnsName google.com

```
$dnsserv = Get-DnsClientServerAddress -InterfaceAlias "Ethernet 5"

$dnsserv[0].ServerAddresses

Clear-DnsClientCache
```

check specific record:
```
Resolve-DnsName www.google.com -Type MX
```

route:
```
Get-NetRoute
```

route for interface alias:
```
Get-NetRoute -InterfaceAlias Wi-Fi
```

netstat:
```
Get-NetTCPConnection
```

have more specified state:
```
Get-NetTCPConnection –State Established
```



