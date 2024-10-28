# filesystems check

**df** - report file system space usage

```
df -h
```

**mount** - mount a filesystem

**strace** - trace system calls and signals

```
strace cksum -tttT /usr/bin/cksum
```

**perf** - Performance analysis tools for Linux

```
perf trace cksum /usr/bin/cksum
```

```
perf stat -e 'ext4:*' -a
```

**fatrace** - report system wide file access events

```
fatrace -f O
```

**pidstat** - Report statistics for Linux tasks

```
pidstat 10
```

### BCC tools

**opensnoop** - Trace files opened

**statsnoop** - Trace calls to stat(2) varieties

**syncsnoop** - Trace sync(2) and variety calls with timestamps

**mmapfiles** - Count mmap(2) files

**scread** - Count read(2) files

**fmapfault** - Count file map faults

**filelife** - Trace short-lived files with their lifespan in seconds

**vfsstat** - Common VFS operation statistics

**vfscount** - ****Count all VFS operations

**vfssize** - Show VFS read/write sizes

**fsrwstat** - Show VFS reads/writes by file system type

**fileslower** - Show slow file reads/writes

**filetop** - Top files in use by IOPS and bytes

**filetype** - Show VFS reads/writes by file type and process

**writesync** - Show regular file writes by sync flag

**cachestat** - Page cache statistics

**writeback** - Show write-back events and latencies

**dcstat** - Directory cache hit statistics

**dcsnoop** - Trace directory cache lookups

**mountsnoop** - Trace mount and umounts system-wide

**xfsslower** - Show slow XFS operations

**xfsdist** - Common XFS operation latency histograms

**ext4dist** - Common ext4 operation latency histograms

**icstat** - Inode cache hit statistics

**bufgrow** - Buffer cache growth by process and bytes

**readahead** - Show read ahead hits and efficiency