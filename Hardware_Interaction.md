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
```
# example with pc with gt 730 nvidia
# linux mint 21.3 kernel 5.15

stencio@stencio-M52AD-M12AD-A-F-K31AD:~$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001287sv00001043sd00000862bc03sc00i00
vendor   : NVIDIA Corporation
model    : GK208B [GeForce GT 730]
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-390 - distro non-free recommended
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-418-server - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```
- If Linux Mint’s Driver Manager only suggests version 390, there are a few possible explanations.
- The most likely one is that the system is identifying your GT 730 as belonging to the family supported by driver 390, even though the PCI ID you showed (10de:1287) corresponds to a GK208B (Kepler).
- The reason only 390 appears in Driver Manager is probably that Mint mainly shows the recommended desktop drivers and does not always expose the “server” packages as a normal choice for desktop users.

# SHOW PCI DEVICES, INCLUDING GPUS
```
lspci | grep -i vga
```
or
```
lspci | grep -E "VGA|3D"
```
* if you see Intel UHD and NVIDIA, the system see both GPUs — so it’s potentially in hybrid mode.
```
glxinfo | grep "OpenGL renderer"     #see witch gpu is redering
```
* another way to gain informations:
```
inxi -G 
```

# DISABLE NOUVEAU DRIVER
```
sudo nano /etc/modprobe.d/blacklist-nouveau.conf          # make fule
                                                          # insert the following 2 rows
blacklist nouveau
options nouveau modeset=0

sudo update-initramfs -u                                  # update initframs
reboot                                                    # reboot system
```
