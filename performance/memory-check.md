# memory check

**swapon** - Swap device usage

**free** - System-wide memory usage

**ps** - Process statistics, including memory usage

**pmap** - Process memory usage by segment

```bash
pmap -x 3785
```

**vmstat** - Various statistics, including memory

```bash
vmstat 1
```

**sar** - Can show page fault and page scanner rates

```bash
sar -B 1
```

### Hardware statistics

**perf** - Memory-related PMC statistics and event sampling

```bash
perf stat -e LLC-loads,LLC-load-misses -a -I 1000
```

### BCC tools

**oomkill** - hows extra info on OOM kill events

**memleak** - Shows possible memory leak code paths

```bash
memleak -p 3126
```

**mmapsnoop** - Traces mmap(2) calls system-wide

**brkstack** - Shows brk() calls with user stack traces

**shmsnoop** - Traces shared memory calls with details

**faults** - Shows page faults, by user stack trace

**ffaults** - Shows page faults, by filename

**vmscan** - Measures VM scanner shrink and reclaim times

**drsnoop** - Traces direct reclaim events, showing latency

```bash
drsnoop -T
```

**swapin** - Shows swap-ins by process

**hfaults** - Shows huge page faults, by process