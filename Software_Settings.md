# UPDATE SYSTEM
in linux mint i use this script, i reserved a line for flatpak update packages
```
# launch this script with sh
echo "================================================================================"
sudo apt-get clean && sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
echo "================================================================================"
flatpak update
echo "================================================================================"
lsb_release -a
echo "================================================================================"
exit
```


# FORCE GRUB TO SHOW
```
sudo nano /etc/default/grub
```
* find following rows and edit them like that:
```
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=5
```
* comment the row with `GRUB_HIDDEN_TIMEOUT=0` with `#`
* save and update GRUB:
```
sudo update-grub         
```
# LINUX MINT HUGE LAG GAMING WITH DRIVER INSTALLED (nvidia)
https://forums.linuxmint.com/viewtopic.php?p=2724077&hilit=game+lag+game+steam#p2724077
it works, i disabled secure boot

# WHICH GRAFIC SERVER IS RUNNING?

```
echo "\$XDG_SESSION_TYPE"
```
to check if both (wayland and xorg) are avaiable on machine:
```
ls /usr/share/wayland-sessions /usr/share/xsessions 2>/dev/null
```
The files in wayland-sessions show Wayland sessions, the ones in xsessions show Xorg sessions. 
You can often pick them on the login screen via a little gear icon, but it depends on your distro and desktop environment.
