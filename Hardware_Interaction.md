# What type of architecture do I have?
```
uname -m
```
or
```
dpkg --print-architecture 
```
* x86_64 --> Architecture 64 bit for CPU intel/AMD
* i686 --> Architecture 32 bit for CPU intel/AMD
* armv7 --> Architecture 32 bit for CPU ARM
* aarch64 --> Architecture 64 bit for CPU ARM

# Which disk was the session booted from?
```
findmnt /
```
* usual output:
```
TARGET SOURCE        FSTYPE OPTIONS
/      /dev/sda2     ext4   rw,...
```
* the source column contains the partition that has the root filesystem in use
* to trace back to the physical disk:
```
lsblk
```
* usual output:
```
sda      931G
├─sda1     1G
└─sda2   930G  /
sdb      500G
└─sdb1   500G
sdc        2T
└─sdc1     2T
```
* in this case the system is booted from the sda disk
