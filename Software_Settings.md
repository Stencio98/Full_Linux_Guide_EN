# UPDATE SYSTEM

in ubuntu i use that commands:
```bash
sudo apt-get clean          # Clear the local APT package cache.
sudo apt-get update         # Refresh the list of available software packages.
sudo apt-get dist-upgrade   # Upgrade installed packages, potentially handling changes to package dependencies.
sudo do-release-upgrade     # Upgrade Ubuntu to a newer Ubuntu release.
sudo apt-get autoremove     # Remove packages that are no longer needed.
sudo snap refresh           # Update applications installed through Snap.
```

in debian:
```bash
sudo apt clean
sudo apt update
sudo apt full-upgrade
sudo apt autoremove
#here u can insert a line for snap or flatpak packages
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
ps -e | grep -E 'Xorg|Xwayland|wayland'
```
to check if both (wayland and xorg) are avaiable on machine:
```
ls /usr/share/wayland-sessions /usr/share/xsessions 2>/dev/null
```
The files in wayland-sessions show Wayland sessions, the ones in xsessions show Xorg sessions. 
You can often pick them on the login screen via a little gear icon, but it depends on your distro and desktop environment.

# VENTOY
https://incastro.altervista.org/guida-completa-a-ventoy-su-linux-installazione-configurazione-e-rischi-da-evitare/

# DISABLE ANIMATION (ubuntu)
```
#disable
gsettings set org.gnome.desktop.interface enable-animations false
```
```
#enable
gsettings set org.gnome.desktop.interface enable-animations true
```
this setting is persistent, you don't have to launch command every pc restart.

# INSTALL FLATPAK ON DEBIAN
```
sudo apt update
sudo apt install flatpak
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

sudo apt install gnome-software-plugin-flatpak #plug in for software manager (based on desktop in use (GNOME, Xfce, ecc..)
```

