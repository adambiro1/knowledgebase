# systemd


## files:

/etc/systemd/system.conf - configuration for the systemd init process.

/lib/systemd/system/ -directory is the default location for unit files

/etc/systemd/system/ - do your changes to unit files here

edit systemd files:

```
sudo systemctl edit --full httpd
```


 do full edit with full option



```
systemctl edit --full sshd.service
```

```
man systemd.exec
```


 >Any unit files in this directory that have the same name as
unit files in /lib/systemd/system/ take precedence.



create unit file:

```
sudo systemctl edit --force --full <something.service>
```

**Types of unit files**


- service: These are the configuration files for services. They replace the
old-fashioned init scripts that we had on the old System V (SysV) systems.

- socket: Sockets can either enable communication between different system
services or they can automatically wake up a sleeping service when it receives a connection request.

- slice: Slice units are used when configuring cgroups. 

- mount and automount: These contain mount point information for filesystems that are controlled by systemd. Normally, they get created automatically, so you shouldn't have to do too much with them.
- target: Target units are used during system startup, for grouping units and for providing well-known synchronization points.
- timer: Timer units are for scheduling jobs that run on a schedule. They
replace the old cron system.
- path: Path units are for services that can be started via path-based activation.
- swap: Swap units contain information about your swap partitions.



### examples

view man pages to config files man:

```
man systemd-system.conf
```

systemctl quick reference:

```
systemctl -h
```

see a list of all of the different states that you can view for the different unit types:

```
systemctl --state=help
```

see the unit files that are installed on the system:

```
systemctl list-unit-files
```

list all running services:

```
sudo systemctl list-units --type=service --state=running
```

if just one individual unit is either enabled or active, you can use the is-enabled and is-active:

```
systemctl is-enabled NetworkManager
```

```
systemctl is-active NetworkManager
```

see the actual running configuration by:

```
systemctl show
```

Use the --property= option to view just one item:

```
systemctl show --property=Virtualization
```

The descriptions for all of the parameters that you can set are spread over several different:

```
man systemd.directives
#systemd.directives - Index of configuration directives
```

```
man systemd.exec - Execution environment configuration
```

enable service and start it:

```
sudo systemctl enable --now httpd
```

analyze with systemd:

```
man systemd-analyze
```

```
systemd-analyze security
```
>analyze exact service (append service name behind security and then adjust it with systemctl edit <service name>)



Get oferview of existing dependecies to current target

```
systemctl list-dependencies
```

Make vim default systemd editor write this to .rc:

```
export SYSTEMD_EDITOR=/bin/vim
```

then reload the .rc file:

```
source .rc
```

## Targets

## Targets/runlevels

poweroff.targetrunlevel 0

rescue.targetrunlevel 1

multi-user.targetrunlevel 3

graphical.targetrunlevel 5

reboot.targetrunlevel 6

list targets:

```
systemctl list-units -t target
```

list inactive targets:

```
systemctl list-units -t target --state inactive
```

list dependencies for target:

```
systemctl list-dependencies graphical.target
```

list dependencies after which target can start:

```
systemctl list-dependencies --after network.target
```

get default target:

```
systemctl get-default
```

or check the symbolic link:

```
ls -l /etc/systemd/system/default.target
```

change default target:

```
sudo systemctl set-default multi-user
```

change it temporary:

```
sudo systemctl isolate multi-user
```

## Timers

list timers:

```
systemctl list-unit-files -t timer
```

get more information to timers:

```
systemctl list-timers
```

get more info about specific timer:

```
systemctl status dnf-makecache.timer
```

get dependencies for  timer:

```
systemctl list-dependencies dnf-makecache.timer
```

check for timing:

```
man systemd.time
```

create a user level timer or service:

```
systemctl edit --user --full --force name.service
```

## Analyzing bootup performance

check how long it took for services to start:

```
systemd-analyze blame
```

see how long it took for each target to start during bootup:

```
systemd-analyze critical-chain
```

## Cgroups 1

List cgroups that are running:

```
systemd-cgls
```

**libcgrop-tools** (tools for cgroups seems not to be found on rhel 9.3)

**lssubsys** - list hierarchies containing given subsystem

reduce cpu quota for user:

```
sudo systemctl set-property user-1001.slice CPUQuota=10%
```

for change to take an effect reload systemd daemon:

```
sudo systemctl daemon-reload
```


>setting user's CPUQuota to 100% doesn't give user 100% usage of each
core. Instead, user would have only about 25% usage of each core. To allow her to have 50% usage of each core, set CPUQuota to 200%. The maximum setting that we can have on this machine with four cores is 400%, which would give her 100% usage of each core.



changes are stored in */etc/systemd/system.control/*

reduce cpu quota for service:

```
sudo systemctl set-property cputest.service CPUQuota=90%
```

check the quota in cgroup filesystem:

```
cat /sys/fs/cgroup/cpu/system.slice/cputest.service/cpu.cfs_quota_us
```

man systemd.resource-control

## Controlling memory usage

limit memory for a user:

```
sudo systemctl set-property --runtime user-1001.slice MemoryMax=1G
```

>without --runtime it is made permanent, this option only makes it for current session, it will disappear after reboot



## Controlling blkio usage

man systemd-

limit users bandwidth:

```
sudo systemctl set-property user-1001.slice BlockIOReadBandwidth="/dev/vda 1M"
```

set the BlockIOReadBandwidth parameter for a service:

```
sudo systemctl set-property httpd.service BlockIOReadBandwidth="/dev/sda 1M"
```

to do the change to some unit add BlockIOReadBandwidth=/dev/vda 1M to [Service] section

## Other options for managing resources:

**ulimit**

>command allows us to dynamically control resource usage for a shell session and for any processes that get started by the shell session:

```
ulimit -a
```

you can either set or lower limits as a normal user, but you need sudo privileges to increase any limits, use the -f option, and specify the file size in terms of the number of 1,024-byte blocks Ten MB works out to be 10,240 blocks, so our command looks like this:

```
ulimit -f 10240
```

## configuration file to set limits

pam_limits

/etc/security/limits.conf or etc/security/limits.d/ directory

add: `user hard fsize 20480`   to the end of a file, it will block user from creating bigger files

## Cgroups 2

set CPUQuota for user:

```
sudo systemctl set-property user-1001.slice CPUQuota=40%
```

reload daemon for changes to take effect:

```
sudo systemctl daemon-reload
```

check changes in user dir:

```
cat /sys/fs/cgroup/user.slice/user-1001.slice/cpu.max
```

change users memory limit:

```
sudo systemctl set-property user-1001.slice MemoryMax=1G
```

reload daemon for changes to take effect:

```
sudo systemctl daemon-reload
```

setting shows up in memory.max file:

```
cat /sys/fs/cgroup/user.slice/user-1001.slice/memory.max
```

limit bandwidth for file transfer for user:

```
sudo systemctl set-property user-1001.slice IOReadBandwidthMax="/dev/vda 1M"
```

see result in:

```
cat /sys/fs/cgroup/user.slice/user-1001.slice/io.max
```

## Services




>The main thing to know about setting limits on services is that each system service has its own subdirectory under the /sys/fs/cgroup/system.slice/



## Setting resource limits on rootless containers

**delegation under cgroup Version 2:**

the default setting, open the /lib/systemd/system/user@.service file, and look for the Delegate= line in the [Service] section.

```
sudo systemctl edit --full user@.service
```

Edit the Delegate= line so that it will look like this:

```
Delegate=pids memory io cpu cpuset
```

Save the file and do a daemon-reload


 if any users are logged in, they might have to log out and log back in again for this to take effect.



create containter with limits:

```
podman run -it --cpu-period=100000 --cpu-quota=50000 ubuntu /bin/
```

inspect the container:

```
podman inspect <container_name>
```

find these lines:

"CpuPeriod": 100000,
"CpuQuota": 50000,

find the attribute file under users cgroup dir:

```
grep -r '50000' /sys/fs/cgroup/user.slice/user-1001.slice/ *
```

attribute file is in

```
/sys/fs/cgroup/user.slice/user-1001.slice/user@1001.service/user.slice/libpod-f2da6646bebce5d02327b1fb3bbbe3b39cb8aefbd9b833d71d97f27c9fab658a.scope/container/cpu.max
```

## Understanding cpuset

**numactl** - Control NUMA policy for processes or shared memory

look at the hardware list:

```
numactl -H
```

assign the Apache service to CPU cores 0 and 2:

```
sudo systemctl set-property httpd.service AllowedCPUs="0 2"
```

assign the Apache service to NUMA node 0:

```
sudo systemctl set-property httpd.service AllowedMemoryNodes=0
```

These two commands will affect the cpuset.cpus and cpuset.mems attribute files:

```
cat /sys/fs/cgroup/system.slice/httpd.service/cpuset.cpus
```

```
cat /sys/fs/cgroup/system.slice/httpd.service/cpuset.mems
```

or edit httpd.service:

```
[Service]

AllowedCPUs=0 2
AllowedMemoryNodes=0
```
## loginctl

loginctl - Control the systemd login manager

 **change logind settings(stuff like like virtual terminal, keep process going after user logs out and so on) in /etc/systemd/logind.conf**



NAutoVTs=6  This sets the number of available virtual terminals.

KillOnlyUsers=user  set it for user to kill his processes when loged out



check user status:

```
loginctl user-status <user>
```

terminate one session for user:

```
sudo loginctl terminate-session 18
```

terminate all sessions for user:

```
sudo loginctl terminate-user <user>
```

