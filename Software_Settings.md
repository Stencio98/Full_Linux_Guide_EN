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
# LINUX MINT HUGE LAG GAMING WITH DRIVER INSTALED (nvidia)
https://forums.linuxmint.com/viewtopic.php?p=2724077&hilit=game+lag+game+steam#p2724077
it works, i disabled secure boot

