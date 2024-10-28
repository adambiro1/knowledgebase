# linux 60 seconds analysis

linux tools plus install **sysstat** package:

```bash
uptime
```

```bash
dmesg | tail
```

```bash
vmstat 1
```

the first line of numbers is the summary since boot (with the exception of the memory counters)

```bash
mpstat -P ALL 1
```

prints per-CPU time broken down into states

```bash
pidstat 1
```

shows CPU usage per process

```bash
iostat -xz 1
```

shows storage device I/O metrics

```bash
free -m
```

```bash
sar -n DEV 1
```

Check interface throughput rxkB/s and txkB/s to see if any limit may have been reached

```bash
sar -n TCP,ETCP 1
```

look at TCP metrics and TCP errors

```bash
top
```

**BCC Tool Checklist:**

```bash
execsnoop
```

shows new process execution by printing one line of output for every execve

```bash
opensnoop
```

prints one line of output for each open(2) syscall (and its variants), including details of the path that was opened

```bash
ext4slower (or btrfs*, xfs*, zfs*)
```

traces common operations from the file system and prints those that exceed a time threshold

```bash
biolatency
```

traces disk I/O latency

```bash
biosnoop
```

prints a line of output for each disk I/O, with details including latency

```bash
cachestat
```

statistics from the file system cache

```bash
tcpconnect
```

output for every active TCP connection

```bash
tcpaccept
```

output for every passive TCP connection

```bash
tcpretrans
```

output for every TCP retransmit packet

```bash
runqlat
```

times how long threads were waiting for their turn on CPU

```bash
profile
```

CPU profiler, a tool you can use to understand which code paths are consuming CPU resources