# networking check

**ss** - Socket statistics

```
ss -tiepm
```

**ip** - ****IP statistics

```
ip -s link
```

**nstat** - Network stack statistics monitor kernel snmp counters and network interface statistics

```
nstat -s
```

**netstat** - Multi-tool for showing network stack statistics and state

**sar** - Multi-tool for showing networking and other statistics

```
sar -n SOCK,TCP,ETCP,DEV 1
```

**nicstat** - Network interface statistics

```
nicstat 1
```

**ethtool** -Network interface driver statistics

```
ethtool -S eth0
```

**tcpdump** -Capture packets for analysis


Many of the prior statistic tools source metrics from /proc files, especially those in /proc/net. This
directory can be explored at the command line:

```
ls /proc/net
```

### BCC tools

**sockstat** - High-level socket statistics

**sofamily** - Count address families for new sockets, by process

**soprotocol** - Count transport protocols for new sockets,by process

**soconnect** - Trace socket IP-protocol connections with details

**soaccept -** Trace socket IP-protocol accepts with details

**socketio** - Summarize socket details with I/O counts

**socksize** - Show socket I/O sizes as per-process histograms

**sormem** - Show socket receive buffer usage and overflows

**soconnlat** - Summarize IP socket connection latency with stacks

**so1stbyte** - Summarize IP socket first byte latency

**tcpconnect** - Trace TCP active connections (connect())

**tcpaccept** - Trace TCP passive connections (accept())

**tcplife** -Trace TCP session lifespans with connection details

**tcptop** - Show TCP send/recv throughput by host

**tcpretrans** -Trace TCP retransmits with address and TCP state

**tcpsynbl** - Show TCP SYN backlog as a histogram

**tcpwin** - Trace TCP send congestion window parameters

**tcpnagle** - Trace TCP nagle usage and transmit delays

**udpconnect** - Trace new UDP connections from localhost

**gethostlatency** - Trace DNS lookup latency via library calls

**ipecn** - Trace IP inbound explicit congestion notification

**superping** - Measure ICMP echo times from the network stack

**qdisc-fq** (...) - Show FQ qdisc queue latency

**netsize** -Show net device I/O sizes

**netieee80211scantxlat** - Show net device transmission latency

**skbdrop** - Trace sk_buff drops with kernel stack traces

**skblife** - Lifespan of sk_buff as inter-stack latency

**ieee80211scan** - Trace IEEE 802.11 WiFi scanning