**lscpu** - display information about the CPU architecture

**getconf** - Query system configuration variables:
```
getconf -a
```

**dmidecode** - DMI table decoder
also in dmi dir:
```
ls /sys/class/dmi/id
```

**lsusb** - list USB devices:
```
lsusb -vv
```
**lspci** - list all PCI devices
```
lspci -vv
```

hwlock package:

**lstopo** - Show the topology of the system
```
lstopo-no-graphics
```

**lshw** - list hardware
```
lshw --short
```

**rasdaemon** - RAS daemon to log the RAS events
```
ras-mc-ctl --help
```