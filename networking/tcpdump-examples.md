# tcpdump_examples

```
-nn : Don’t resolve hostnames *or* port names
```

```
-S : Get the entire packet.
```

```
-X : Get hex output.
```

```
**-X** : Show the packet’s *contents* in both [**hex**](https://en.wikipedia.org/wiki/Hexidecimal?utm_source=danielmiessler.com&utm_medium=referral&utm_campaign=a-tcpdump-tutorial-with-examples) and [**ASCII**](https://en.wikipedia.org/wiki/Ascii?utm_source=danielmiessler.com&utm_medium=referral&utm_campaign=a-tcpdump-tutorial-with-examples).
```

```
**-XX** : Same as **X**, but also shows the ethernet header.
```

```
**-D** : Show the list of available interfaces
```

```
**l** : Line-readable output (for viewing as you save, or sending to other commands)
```

```
**-q** : Be less verbose (more quiet) with your output.
```

```
**-t** : Give human-readable timestamp output.
```

```
**-tttt** : Give maximally human-readable timestamp output.
```

```
**-i eth0** : Listen on the eth0 interface.
```

```
**-vv** : Verbose output (more v’s gives more output).
```

```
**-c** : Only get *x* number of packets and then stop.
```

```
**-s** : Define the *snaplength* (size) of the capture in bytes. Use -s0 to get everything, unless you are intentionally capturing less.
```

```
**-S** : Print absolute sequence numbers.
```

```
**-e** : Get the ethernet header as well.
```

```
**-q** : Show less protocol information.
```

```
**-E** : Decrypt IPSEC traffic by providing an encryption key.
```

<aside>
💡 combinations

**AND:** *and* or &&

**OR:** *or* or ||

**EXCEPT:** *not* or !

</aside>

examples

```
sudo tcpdump -i eth0 -A -n port 80 | grep "angular"
```

```
tcpdump -nn -s 0 -i bond0 -w /var/tmp/${HOSTNAME}_$(date +%d_%m_%Y-%H_%M_%S-%Z).pcap
```

get us HTTPS traffic:

```
tcpdump -nnSX port 443
```

Capture Credentials in Plain Text:

```
tcpdump -A -i eth0 'port http or port ftp or port telnet' | grep -i 'user\|pass\|login'
```

Monitor Traffic to a Suspicious Domain:

```
tcpdump -i eth0 dst host suspicious.com
```

Capture Traffic from a Specific IP Range

```
tcpdump src net {IP_RANGE_OF_COUNTRY}
```

Monitor SMB Traffic:

```
tcpdump -nn -i eth0 port 445
```

Capture TCP RESET-ACK Packets:

```
tcpdump 'tcp[13] = 41'
```

find traffic by ip:

```
tcpdump host 1.1.1.1
```

Filtering by Source and/or Destination

```
tcpdump src 1.1.1.1tcpdump dst 1.0.0.1
```

Finding Packets by Network To find packets going to or from a particular network or subnet, use the net option:

```
tcpdump net 1.2.3.0/24
```

Get Packet Contents with Hex Output:

```
tcpdump -c 1 -X icmp
```

Show Traffic Related to a Specific Port:

```
tcpdump  port 3389
```

```
tcpdump  src port 1025
```

Show Traffic of One Protocol:

```
tcpdump icmp
```

Show only IP6 Traffic:

```
tcpdump ip6
```

Find Traffic Using Port Ranges:

```
tcpdump  portrange 21-23
```

Find Traffic Based on Packet Size:

```
tcpdump 'len > 32 and len < 64'
```

Reading / Writing Captures to a File (pcap):

```
tcpdump  port 80 -w capture_file
```

```
tcpdump  -r capture_file
```

Raw Output View:

```
tcpdump -ttnnvvS
```

From specific IP and destined for a specific Port:

```
tcpdump -nnvvS src 10.5.2.3 and dst port 3389
```

From One Network to Another:

```
tcpdump -nvX src net 192.168.0.0/16 and dst net 10.0.0.0/8 or 172.16.0.0/16
```

Non ICMP Traffic Going to a Specific IP:

```
tcpdump dst 192.168.0.2 and src net and not icmp
```

Traffic From a Host That Isn’t on a Specific Port:

```
tcpdump -vv src mars and not dst port 22
```

use () to group expressions such as host, port, net, etc:

```
tcpdump 'src 10.0.2.4 and (dst port 3389 or 22)'
```

Isolate TCP Flags:

```
tcpdump 'tcp[13] & 4!=0'tcpdump 'tcp[tcpflags]  == tcp-rst'
```

Isolate TCP SYN flags:

```
tcpdump 'tcp[13] & 2!=0'tcpdump 'tcp[tcpflags]  == tcp-syn'
```

Isolate packets that have both the SYN and ACK flags set:

```
tcpdump 'tcp[13]=18'
```

Isolate TCP URG flags:

```
tcpdump 'tcp[13] & 32!=0'tcpdump 'tcp[tcpflags]  == tcp-urg'
```

Isolate TCP ACK flags**:**

```
tcpdump 'tcp[13] & 16!=0' tcpdump 'tcp[tcpflags]  == tcp-ack'
```

Isolate TCP PSH flags**:**

```
tcpdump 'tcp[13] & 8!=0' tcpdump 'tcp[tcpflags]  == tcp-push'
```

Isolate TCP FIN flags**:**

```
tcpdump 'tcp[13] & 1!=0'tcpdump 'tcp[tcpflags]  == tcp-fin'
```

Find HTTP User Agents:

```
tcpdump -vvAls0 | grep 'User-Agent:'
```

Cleartext GET Requests**:**

```
tcpdump -vvAls0 | grep 'GET'
```

Find HTTP Host Headers:

```
tcpdump -vvAls0 | grep 'Host:'
```

Find HTTP Cookies:

```
tcpdump -vvAls0 | grep 'Set-Cookie|Host:|Cookie:'
```

Find SSH Connections:

This one works regardless of what port the connection comes in on, because it’s getting the banner response.

```
tcpdump 'tcp[(tcp[12]>>2):4] = 0x5353482D'
```

Find DNS Traffic:

```
tcpdump -vvAs0 port 53
```

Find FTP Traffic**:**

```
tcpdump -vvAs0 port ftp or ftp-data
```

Find NTP Traffic**:**

```
tcpdump -vvAs0 port 123
```

Find Cleartext Passwords**:**

```
tcpdump port http or port ftp or port smtp or port imap or port pop3 or port telnet -lA | egrep -i -B5 'pass=|pwd=|log=|login=|user=|username=|pw=|passw=|passwd=|password=|pass:|user:|username:|password:|login:|pass |user ' 
```

Find Traffic With Evil Bit:

```
tcpdump 'ip[6] & 128 != 0'
```