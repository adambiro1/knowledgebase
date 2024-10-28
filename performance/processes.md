**ps**

show exact command that started the process:
```
ps -ef
```
show hierarchy between parent and child processes:
```
ps fax
```
show zombie processes:
```
ps aux | grep defunct
```
custom output:
```
ps ax --format pid,%mem,cmd --sort -%mem
```
```
ps axo user,pid,ppid,comm,psr
```
**sar** - Collect, report, or save system activity information:

make an output file:
```
sar -o report.out 1 3
```
**tuned** - dynamic adaptive system tuning daemon 

**lscpu** - display information about the CPU architecture 

**chcpu** - configure CPUs


**perf** - Performance analysis tools for Linux

```
perf top
```

Count the events for a command:
```
perf stat ls
```
perf stat operates in per-thread mode. To change to CPU-wide event counting, pass the -a:
```
perf stat -a ls
```

Attach perf stat to a running process:
```
perf stat -p ID1,ID2 sleep seconds
```

**numactl** - Control NUMA policy for processes or shared memory

display an overview of system topology:
```
numactl --hardware
```

**numastat** - Show per-NUMA-node memory statistics for processes and the operating system \(install numactl package\):

```
numastat -c -z -m -n
```

```
numastat -czs libvirt kvm qemu
```

```
watch -n1 numastat
```

```
watch -n1 --differences=cumulative numastat
```

**turbostat** - Report processor frequency and idle statistics
>/proc/interrupts file displays the interrupt request (IRQ) number, the number of similar interrupt requests handled by each processor in the system, the type of interrupt sent, and a comma-separated list of devices that respond to the listed interrupt request

**pqos, pqos-msr, pqos-os** - Intel(R) Resource Director Technology/AMD PQoS monitoring and control tool

install it:
```
dnf install intel-cmt-cat
```

>x86_energy_perf_policy tool allows administrators to define the relative importance of performance and energy efficiency. This information can then be used to influence processors that support this feature when they select options that trade off between performance and energy efficiency.

**qtaskset** - set or retrieve a process's CPU affinity

**pstree** - show tree of all processes

**tuna** - program for tuning running processes
```
tuna -h
```

view the current policies and priorities:
```
tuna --show_threads
```
**powertop** - a power consumption and power management diagnosis tool

**whowatch** - whowatch - console, interactive, process and users monitoring tool

**tapestat** - Report tape statistics

**cifsiostat** - Report CIFS statistics