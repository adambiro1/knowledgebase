# linux 60 seconds analysis

linux tools plus install **sysstat** package:

```
uptime
```

```
dmesg | tail
```

```
vmstat 1
```

the first line of numbers is the summary since boot (with the exception of the memory counters)

```
mpstat -P ALL 1
```

prints per-CPU time broken down into states

```
pidstat 1
```

shows CPU usage per process

```
iostat -xz 1
```

shows storage device I/O metrics

```
free -m
```

```
sar -n DEV 1
```

Check interface throughput rxkB/s and txkB/s to see if any limit may have been reached

```
sar -n TCP,ETCP 1
```

look at TCP metrics and TCP errors

```
top
```

**BCC Tool Checklist:**

```
execsnoop
```

shows new process execution by printing one line of output for every execve

```
opensnoop
```

prints one line of output for each open(2) syscall (and its variants), including details of the path that was opened

```
ext4slower (or btrfs*, xfs*, zfs*)
```

traces common operations from the file system and prints those that exceed a time threshold

```
biolatency
```

traces disk I/O latency

```
biosnoop
```

prints a line of output for each disk I/O, with details including latency

```
cachestat
```

statistics from the file system cache

```
tcpconnect
```

output for every active TCP connection

```
tcpaccept
```

output for every passive TCP connection

```
tcpretrans
```

output for every TCP retransmit packet

```
runqlat
```

times how long threads were waiting for their turn on CPU

```
profile
```

CPU profiler, a tool you can use to understand which code paths are consuming CPU resources