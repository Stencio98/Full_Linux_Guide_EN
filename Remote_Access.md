# SAMBA
install samba:
```
sudo apt install samba
```

make the folder that will be shared:
```
mkdir -p ~/shared_folder
chmod 777 ~/shared_folder
```

edit samba configuration:
```
sudo nano /etc/samba/smb.conf
```

add "shared_folder":
```

[shared_folder]
## 2 space left margin
  comment = samba linux
  path = /home/user_name/shared_folder
  read only = no
  browsable = yes

```

reboot samba service:
```
sudo service smbd restart
```
config firewall (if active):
```
sudo ufw allow samba
```

network sharing access: on Windows we can type the IP address of the Linux computer in the File Explorer address bar
if you can't access it, try using a username and password:
```
sudo smbpasswd -a user_name
```
auto run samba when pc turn on:
```
sudo systemctl enable smbd
sudo systemctl enable nmbd
```
```
sudo systemctl start smbd
sudo systemctl start nmbd
```
to see samba status:
```
sudo service smbd status
```

# SSH LAN GUIDE
__a == client; b == server__
install ssh service on __b__ (better both machines):
```
sudo apt install openssh-server
```
to find ip address of __b__ from __b__ shell :
```
ip addr
```
The firewall (if present) must allow connections (on port 22), it can be set up like this __b__ :
```
sudo ufw allow ssh
```
to connect from __a__ shell:
```
ssh b_username@b_ip_address
#then shell will change name and we will bw inside b
```
to copy a file from __a__ to __b__ and vice versa, we open a new shell on __a__ and use scp:
`scp /percorso/file.txt b_username@b_ip_address:/home/b_username/destinazione/ #a --to--> b` 
`scp b_username@b_ip_address:/home/b_username/file_da_copiare.txt . #b --to--> a`

# TAILSCALE 
to be continued ...
install taiscale:
```
curl -fsSL https://tailscale.com/install.sh | sh

```
After installing Tailscale, run:

```bash
tailscale up
```

This logs in and connects the device.
Check status
```bash
tailscale status
```
Get your Tailscale IP
```bash
tailscale ip -4
```
to be sure tailscale will turn on automatically at pc start:
```
sudo systemctl enable --now tailscaled
```
stop service and disable auto run:
```
sudo systemctl stop tailscaled
sudo systemctl disable tailscaled
```
# SSH WITH TAILSCALE
```bash
sudo tailscale up --ssh
```
--ssh: enable Tailscale SSH, that is, SSH access through the Tailscale network, using Tailscale's rules instead of classic SSH exposed on the Internet

# SCRIPT FOR CHECK STATUS SAMBA AND TAILSCALE
```
# launch with sh
echo "==============================="
echo "=== CHECK SAMBA E TAILSCALE ==="
echo "==============================="
echo "\n\e[1msmbd (samba)\e[0m"
systemctl is-active smbd
echo "\n\e[1mnmbd (samba)\e[0m"
systemctl is-active nmbd
echo "\n\e[1mTailscale IP\e[0m"
tailscale ip -4
echo "\n\e[1mtailscale\e[0m"
systemctl is-active tailscaled
echo "\n\e[1mcheck tailscale ssh\e[0m"
tailscale debug prefs | grep -i ssh
echo "\n\e[1mTailscale status\e[0m"
tailscale status


```
