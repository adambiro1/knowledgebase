# CPU check

**uptime** - Shows load averages and system uptime

**top** - Shows CPU time by process and CPU mode times system-wide

**mpstat** - Report processors related statistics

```
mpstat -P ALL 1
```

View the top 10 most-CPU-consuming processes:
```
ps -L aux | sort -nr -k 4 | head -10
```
### Hardware statistics

**perf** - Profiles (timed sampling) of stack traces and event statistics and tracing of PMCs, tracepoints, USDT probes, kprobes, and uprobes

**Ftrace** - Reports kernel function count statistics and event tracing of kprobes and uprobes

## BCC tools

**execsnoop** - new process execution

**exitsnoop** - Shows process lifespan and exit reason

**runqlat** - Summarizes CPU run queue latency

**runqlen** - Summarizes CPU run queue length

**runqslower** - Prints run queue waits slower than a threshold

**cpudist** - Summarizes on-CPU time

**cpufreq** - Samples CPU frequency by process

**profile** - Samples CPU stack traces

**offcputime** - Summarizes off-CPU stack traces and times

**syscount** - Counts system calls by type and process

**argdist** - Can be used for syscall analysis

**trace** - Can be used for syscall analysis

**funccount** - Counts function calls

**softirqs** - Summarizes soft interrupt time

**hardirqs** - Summarizes hard interrupt time

**smpcalls** - Times SMP remote CPU calls

**llcstat** - Summarizes LLC hit ratio by process