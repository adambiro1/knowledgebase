# Networking on Windows
## CMD tips:

``` 
wmic useraccount where name="UID" get SID

wmic product where "name like'%%office%%'" get name,version
``````
 

List logged in users: 
```
query session
```

 

```
C:\Users\user>query session

SESSIONNAME       USERNAME                 ID  STATE   TYPE        DEVICE

services                                    0  Disc

>console           user                  1  Active


…    logoff 1  (number is query )
```

Change cmd prompt look:
 
```
C:\Users\user>prompt $D$S$T$_$V$_$P$_$G

Fri 08/04/2023  8:05:02.82
Microsoft Windows [Version 10.0.19044.3208]

C:\Users\user
>prompt

 C:\Users\user>

```
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
show interfaces:
```
netsh interface show interface
```
Configure Specific Network Interface:
```
netsh interface ipv4 set address "<interface name>" static <IP address> <subnet mask> <default gateway>
```

show wifi profiles:
```
netsh wlan show profiles
```

show wifi password:
```
netsh wlan show profile name="<profile name>" key=clear
```

## Powershell:

list ip configuration:
```
Get-NetIPConfiguration
```

list all Network Adapters:
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

more detailed ping:
```
Test-NetConnection www.google.com -InformationLevel Detailed
```

also specify hops:
```
Test-NetConnection -ComputerName www.google.com -Hops 5
```

tracert with PowerShell:
```
Test-NetConnection www.google.com –TraceRoute
```

check opend ports:
```
Test-NetConnection -ComputerName www.google.com -Port 80
#or
Test-NetConnection -ComputerName www.google.com -CommonTCPPort HTTP
```

check dns *nslookup in cmd*:
```
Resolve-DnsName www.google.com
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




**DnsClient**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/dnsclient/?view=windowsserver2019-ps)

 
**NetAdapter**

[cmdlets](ttps://learn.microsoft.com/en-us/powershell/module/netadapter/?view=windowsserver2019-ps)

 
**NetConnection**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/netconnection/?view=windowsserver2019-ps)
 

**NetEventPacketCapture**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/neteventpacketcapture/?view=windowsserver2019-ps)

 
**NetLldpAgent**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/netlldpagent/?view=windowsserver2019-ps)


**NetNat**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/netnat/?view=windowsserver2019-ps)


**NetQoS**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/netqos/?view=windowsserver2019-ps)


**NetSecurity**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/netsecurity/?view=windowsserver2019-ps)

 
**NetTCPIP**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/nettcpip/?view=windowsserver2019-ps)

 
**NetworkConnectivityStatus**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/networkconnectivitystatus/?view=windowsserver2019-ps)

 
**NetworkController**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/networkcontroller/?view=windowsserver2019-ps)

 
**NetworkControllerDiagnostics**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/networkcontrollerdiagnostics/?view=windowsserver2019ps)

 
**NetworkSwitchManager**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/networkswitchmanager/?view=windowsserver2019-ps)

 
**NFS**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/nfs/?view=windowsserver2019-ps)

 
**pki**

[cmdlets](https://learn.microsoft.com/en-us/powershell/module/pki/?view=windowsserver2019-ps)
 

**SmbShare**
 
[cmdlets](https://learn.microsoft.com/en-us/powershell/module/smbshare/?view=windowsserver2019-ps)

 
**TLS**
 
[cmdlets](https://learn.microsoft.com/en-us/powershell/module/tls/?view=windowsserver2019-ps)

 
**VpnClient**


[cmdlets](https://learn.microsoft.com/en-us/powershell/module/vpnclient/?view=windowsserver2019-ps>)