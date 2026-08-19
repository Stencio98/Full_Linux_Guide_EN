# SAMBA
* install samba:
```
sudo apt install samba
```

* make the folder that will be shared:
```
mkdir -p ~/shared_folder
chmod 777 ~/shared_folder
```

* edit samba configuration:
```
sudo nano /etc/samba/smb.conf
```

* add "shared_folder":
```

[shared_folder]
## 2 space left margin
  comment = samba linux
  path = /home/user_name/shared_folder
  read only = no
  browsable = yes

```

* reboot samba service:
```
sudo service smbd restart
```
* config firewall (if active):
```
sudo ufw allow samba
```

* network sharing access: on Windows we can type the IP address of the Linux computer in the File Explorer address bar
* if you can't access it, try using a username and password:
```
sudo smbpasswd -a user_name
```
* auto run samba when pc turn on:
```
sudo systemctl enable smbd
sudo systemctl enable nmbd
```
```
sudo systemctl start smbd
sudo systemctl start nmbd
```
* to see samba status:
```
sudo service smbd status
```
