# disk I/O check

**iostat** - Report Central Processing Unit (CPU) statistics and input/output statistics for devices and partitions

```
iostat -dxz 1
```

**blktrace** - generate traces of the i/o traffic on block devices

```
btrace /dev/nvme2n1
```

enable SCSI event logging:

```
sysctl -w dev.scsi.logging_level=0x1b6db6db
```

or

```
echo 0x1b6db6db > /proc/sys/dev/scsi/logging_level
```

### BCC tools

**biolatency** - Summarize block I/O latency as a histogram
**biosnoop** - Trace block I/O with PID and latency
**biotop** -Top for disks: summarize block I/O by process
**bitesize** -Show disk I/O size histogram by process
**seeksize** -Show requested I/O seek distances
**biopattern** - Identify random/sequential disk access patterns
**biostacks** -Show disk I/O with initialization stacks
**bioerr** - Trace disk errors
**mdflush** - Trace md flush requests
**iosched** - Summarize I/O scheduler latency
**scsilatency** -Show SCSI command latency distributions
**scsiresult** - Show SCSI command result codes
**nvmelatency** - Summarize NVME driver command latency