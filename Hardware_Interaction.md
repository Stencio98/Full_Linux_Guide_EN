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

# MOUNT SECOND HDD AS ARCHIVE
* let's identify disks and their loro UUID
```
:$ sudo blkid
/dev/sda1: UUID="XXXX-XXXX" TYPE="ext4"
/dev/sdb1: UUID="YYYY-YYYY" TYPE="ext4"
```
* edit following file:
```
sudo nano /etc/fstab
```
which contains the information needed to set up the system's storage devices, so we add the line:
```
UUID=YYYY-YYYY /mnt/dati ext4 defaults 0 2
```
at the end of the file, replacing UUID with the disk's UUID, /mnt/dati with the desired mount point (create the directory first if it doesn't exist), and ext4 with the disk's file system type, if needed. If we're not sure about the file system type, we can use `auto` as the option.

* make mnt point:
```
sudo mkdir -p /mnt/dati
```
* we test the mounting with the following command that tries to mount all the file systems defined in `/etc/fstab`. If there are no errors, the disk will be mounted correctly:
```
sudo mount -a
```
* use `df` to see if the disk is rightlt mounted:
```
df -h
```
* if we want `samba` to point to the new mount point (if samba is not yet connected to the drive or the mount point has become different from the previous one and so samba “can’t find” the old shared folder):
```
[Dati]
  path = /mnt/dati
  available = yes
  valid users = tuo_utente
  read only = no
  browsable = yes
  public = yes
  writable = yes
```
* reboot `samba`:
```
sudo systemctl restart smbd
```
