# WHAT TYPE OF ARCHITECTURE DO I HAVE?
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

# WHICH DISK WAS THE SESSION BOOTED FROM?
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

# COMPATIBLE DRIVERS FOR THE GPU

- If Linux Mint’s Driver Manager only suggests version 390, there are a few possible explanations.
- The most likely one is that the system is identifying your GT 730 as belonging to the family supported by driver 390, even though the PCI ID you showed (10de:1287) corresponds to a GK208B (Kepler).
- The reason only 390 appears in Driver Manager is probably that Mint mainly shows the recommended desktop drivers and does not always expose the “server” packages as a normal choice for desktop users.
