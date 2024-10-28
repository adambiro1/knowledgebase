# linux-kernel


lists currently loaded kernel modules:

```
lsmod
```

displays information about kernel modules:

```
modinfo <module name>
```

load kernel modules, including all of their dependencies:

```
modprobe <module name>
```

unloads kernel modules, considering kernel module dependencies

```
modprobe -r <module name>
```

upgrade kernel:

```
dnf upgrade kernel
```
